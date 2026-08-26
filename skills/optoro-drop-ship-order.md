---
name: optoro-drop-ship-order
description: Find resale inventory in the Optoro RMS, place a drop-ship order against it, track the shipment, and cancel while it is still reversible.
api: Optoro Drop Ship API
operations:
  - oauthTokenFetch
  - listingsIndex
  - listingsShow
  - listingsUpdate
  - ordersCreate
  - batchOrdersCreate
  - OrdersIndex
  - ordersShow
  - ordersUpdate
  - ordersCancel
  - shipmentsIndex
  - shipmentsShow
  - shipmentsShowByIdentifier
source: https://developer.optoro.com/openapi/drop_ship/openapi
generated: '2026-08-26'
method: generated
---

# Order returned inventory through Drop Ship

The Drop Ship API (v6.0, `openapi/optoro-drop-ship-openapi.yml`) lets you fulfil orders directly from
returned and excess units and lots held in the Optoro RMS. Base host `https://drop-ship.optiturn.com`
(sandbox `https://drop-ship.sandbox.optiturn.com`).

## Steps

1. **Authenticate** — see `optoro-authenticate`.
2. **Browse inventory.** `GET /listings` (`listingsIndex`) — paginate with `page` and `per_page`.
   `GET /listings/{id}` (`listingsShow`) returns one listing with its `lot`, `channel`, `condition` and
   `quantity`; the lot carries `manifest_items[]` with `sku`, `upc`, `condition`, `item_title`,
   `manufacturer`, `category_lineage` and `vendor_*`.
3. **Adjust availability if you own it.** `PUT /listings/{id}` (`listingsUpdate`) updates listing quantity.
4. **Place the order.** `POST /orders` (`ordersCreate`) with `order_items[]`, `shipping_address` and
   `billing_address`. For volume use `POST /batch/orders` (`batchOrdersCreate`) — watch for `413` and split
   the batch if the body is too large.
5. **Track it.** `GET /orders` (`OrdersIndex`), `GET /orders/{id}` (`ordersShow`),
   `GET /shipments/identifier/{id}` (`shipmentsShowByIdentifier`) for the shipments belonging to an order,
   and `GET /shipments/{id}` (`shipmentsShow`) for `carrier`, `tracking_number`, `shipping_method` and
   `billed_weight`.
6. **Amend or cancel.** `PUT /orders/{id}` (`ordersUpdate`) and `DELETE /orders/{id}` (`ordersCancel`),
   both returning `204`.

## Reversibility — the window is a status, not a clock

`ordersCancel` "Cancels the lot order that matches the identifier that is included in the url path **from
pending_payment status**". Once the order leaves `pending_payment` the call fails with `422` and the message
`Order status should be pending_payment`. **Check `ordersShow` for the current status before assuming an
order can still be pulled back**, and treat a `422` on cancel as final rather than retrying it.

Cancellation initiated on Optoro's side arrives as the `drop_shipment_cancellation` or
`drop_shipment_partial_cancellation` webhook — see `asyncapi/optoro-webhooks.yml`.

## Failure handling

- `400` bad request · `401` refresh token and retry once · `404` unknown identifier ·
  `413` request too large, split the batch · `422` validation, read `message` and `errors[]` ·
  `5XX` retry three times with exponential backoff.

## Caution

There is **no idempotency key** on `ordersCreate` or `batchOrdersCreate`. A retried create after an
ambiguous timeout can produce a duplicate order. Before retrying, call `OrdersIndex` / `ordersShow` and
reconcile on your own `client_identifier` before firing again.
