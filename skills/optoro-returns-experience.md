---
name: optoro-returns-experience
description: Wire a retailer's order data into the Optoro returns portal and consume the RMA, exchange and variant callbacks that come back.
api: Optoro Returns Experience APIs
operations:
  - oauthTokenFetch
  - returns_portal_orders
  - rmas
  - exchange_orders
  - variants
source: https://developer.optoro.com/content/rx_integration_guide
generated: '2026-08-26'
method: generated
---

# Run the shopper returns loop

This flow is **bidirectional**. The retailer pushes order state to Optoro; Optoro pushes RMA events and
exchange requests back to endpoints the retailer hosts. Both halves have to exist before returns work.

## Outbound — you call Optoro

1. **Authenticate** — see `optoro-authenticate`.
2. **Post order snapshots.** `POST https://orders.optiturn.com/returns_portal_orders`
   (`returns_portal_orders`, `openapi/optoro-returns-portal-orders-openapi.yml`, v3.0.0) with the FULL
   snapshot of the order — `orders`, `items[]`, `customer`, `refunds[]`.
   - Post at the first shipped event of an order.
   - Backfill roughly six months of history at implementation.
   - Re-post the full snapshot on every lifecycle event: fulfillments, transactions, adjustments, line-item
     modifications, and refunds. As close to real time as possible.
   - Response is `200`. There is no partial-update endpoint — the snapshot IS the update.

## Inbound — Optoro calls you

3. **RMA webhook.** Optoro `POST`s the RMAs message (`rmas`, `openapi/optoro-rmas-openapi.yml`, v5.0.0)
   to a URL you supply, with header `X-Optiturn-Id` (your tenant) and `X-Optiturn-Api-Version`.
   Fires when the shopper initiates a return, when carrier tracking appears, when the carrier scans the
   return, on drop-off or pick-up, on warehouse receipt, and after you post refund details.
   Read `items[].order_identifier`, `order_line_item_identifier`, `refund_type`, `package_tracking_status`,
   and when present `tracking_number`, `original_order_identifier`, `exchange_order_identifier`,
   `receiving_status`, `warehouse_receipt_condition`.
4. **Exchange Variants endpoint.** Optoro `GET`s `/sku/{parent_sku}/variants` (`variants`,
   `openapi/optoro-variants-openapi.yml`) from you to show the shopper what an even exchange can be.
5. **Exchange Orders endpoint.** Optoro `POST`s an exchange order (`exchange_orders`,
   `openapi/optoro-exchange-orders-openapi.yml`, v2.0.0) when the shopper confirms an exchange or an instant
   gift-card refund. **Your endpoint owns all tax and shipping calculation, and must be idempotent keyed on
   `original_order_id` — only one exchange order may exist per `original_order_id`.**

## Webhook contract you must honour

- Delivery is **at-least-once** and **out of order**. De-duplicate; use the message timestamp to sequence.
- Respond `200` on success. If a message is irrelevant or unparseable to you, **still respond `2xx`** —
  Optoro explicitly asks you not to return `400`/`422`, because that generates noise in its monitoring.
- Respond `5xx` (500/502/503/504) only when you genuinely want a retry. Optoro retries with exponential
  backoff for up to **32 hours**; messages are retained **30 days**. A `401` triggers re-authentication and
  one retry.
- Authenticate the callback with Basic Auth, OAuth 2, AWS SigV4, or an API key header — configured with
  Optoro Client Success, secrets delivered encrypted.
- TLS 1.2 minimum, certificate signed by a globally trusted CA, **intermediates installed on your server**
  (Optoro will not install them).

## Note

Version pinning differs per callback: the RMAs v5 spec pins `X-Optiturn-Api-Version: 3`, Exchange Orders
accepts `1` or `2`, Exchange Variants accepts `1`. Read the individual spec rather than assuming a shared value.
