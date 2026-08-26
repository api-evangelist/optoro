---
name: optoro-warehouse-events
description: Feed inbound shipments and warehouse state into Optoro and consume the disposition and outbound-shipment events it emits.
api: Optoro Returns Processing APIs
operations:
  - oauthTokenFetch
  - createExternalBinChange
  - showExternalBinChange
  - upsertFacility
  - vendorUpdate
  - dispositions
  - final_dispositions
  - outbound_asns
source: https://developer.optoro.com/content/rm_integration_guide
generated: '2026-08-26'
method: generated
---

# Operate the returns warehouse surface

## Set up the network

1. **Authenticate** — see `optoro-authenticate`.
2. **Register facilities.** `POST /facilities` (`upsertFacility`,
   `openapi/optoro-facilities-openapi.yml`, version `2024-08-08`) on
   `https://facilities.optiturn.com` — create-or-update a store or warehouse.
3. **Register RTV vendors.** `POST /vendor_updates` (`vendorUpdate`,
   `openapi/optoro-rtv-openapi.yml`, v2.0.0) on `https://rtv.optiturn.com` — vendor policies and
   return-to-vendor agreements. Required only if you use RTV functionality. Returns `201` or `202`.

## Announce inbound shipments

4. **Create an ASN.** `POST /asns` on `https://asn.optiturn.com`
   (`openapi/optoro-asn-openapi.yml`) with `asn_number`, `asn_type`, `carrier`, `tracking_number`,
   `ship_date`, `from`, `to` and `cartons[]`; each carton carries `details[]` with `sku`, `upc`, `asin`,
   `condition`, `quantity`, `return_reason`, `return_date`, `unit_identifier`, `vendor_identifier`. Returns `202`.
5. **Amend it.** `PUT /asns/{asn-number}` — addressed by the ASN number you supplied, so this is a
   natural-key upsert. Also `202`.
6. **Real-time receipt.** `POST /inventory_receipt` (`openapi/optoro-inventory-receipt-openapi.yml`).

## Move units in the warehouse

7. **Bin change.** `POST /external_bin_changes` (`createExternalBinChange`) on `https://optiturn.com`
   (sandbox `https://sandbox.optiturn.com`), scoped `write:external_bin_changes`. Returns `201`.
8. **Read one back.** `GET /external_bin_changes/{id}` (`showExternalBinChange`), scoped
   `read:external_bin_changes`. This is the only read-your-write pair Optoro publishes outside Drop Ship —
   use it to confirm a move landed.

## Consume the events Optoro sends you

9. **Disposition Update** (`dispositions`) — a unit's `from_disposition`/`to_disposition`,
   `from_condition`/`to_condition`, `from_sku`/`to_sku`, `location_identifier`, `optiturn_lp`,
   `warehouse_identifier` or `store_identifier`, `user_login`, `timestamp`.
10. **Final Disposition** (`final_dispositions`) — the terminal outcome for a unit.
11. **Outbound ASN** (`outbound_asns`) — outbound shipments and stock transfers, with `carrier` and
    `carrier_payment_type`.

All three are Optoro-to-you POSTs with the same webhook contract described in
`asyncapi/optoro-webhooks.yml`: at-least-once, unordered, `2xx` to acknowledge, 32-hour retry, 30-day retention.

## Failure handling

`400` bad request · `401` refresh token, retry once · `422` read `message` + `errors[{field, code}]` ·
`500`/`502`/`503`/`504` retry three times with exponential backoff, then escalate to Optoro Client Support.

## Caution

None of these writes has a reversal operation. Facility, vendor and ASN updates are last-writer-wins upserts
on a natural key; a bin change has no undo. Read the current state before overwriting it.
