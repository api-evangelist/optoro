---
name: optoro-sync-catalog
description: Publish or update product master data in Optoro so returned units can be dispositioned, routed and resold correctly.
api: Optoro Returns Processing APIs
operations:
  - oauthTokenFetch
  - catalogEntryUpdate
source: https://developer.optoro.com/openapi/catalogs/openapi
generated: '2026-08-26'
method: generated
---

# Keep the Optoro catalog current

The Catalogs API is the product master Optoro reasons over. Disposition decisions, routing, reporting and
resale channel eligibility all read from it, so a stale or partial catalog degrades every downstream outcome.

## Steps

1. **Authenticate** — see `optoro-authenticate`. Base host `https://catalogs.optiturn.com`
   (sandbox `https://catalogs.sandbox.optiturn.com`).
2. **Upsert an entry.** `POST /catalog_entry_updates` (`catalogEntryUpdate`,
   `openapi/optoro-catalogs-openapi.yml`, version `2023-08-01`). This is a create-or-update on the
   retailer's SKU.
3. **Send identifiers in the modern shape.** As of `2023-08-01` the top-level `upc`, `upcs` and `asin`
   fields are **rejected**. Use `product_identifiers.items[]`, each entry `{value, type}` where `type` is
   one of `upc` | `asin` | `generic`. Set `update_behavior` to control whether the submitted identifiers
   `append` to or `replace` the existing set.
4. **Respect channel exclusivity.** `allowed_channels` and `disallowed_channels` are mutually exclusive —
   sending both is a validation failure.
5. **Verify.** A `200` means the entry was accepted.

## Critical caution — this write is not reversible

Optoro performs minimal validation and treats what you send as truth. The docs state: "Null or empty values
will be saved and can overwrite previously submitted data. If this is not desired then omit the field from
the update request." There is no delete and no undo. **Omit fields you do not intend to change**, and retain
the prior state yourself if you may need to restore it.

## Failure handling

- `400` — unparseable JSON. Fix the payload; do not retry unchanged.
- `401` — refresh the token and retry once.
- `422` — read `message` and the `errors[]` array of `{field, code}`; correct and resend.
- `5XX` — retry three times with exponential backoff, then escalate to Optoro Client Support.

## Notes

- Bulk/initial loads: Optoro recommends a CSV file transfer for the first large catalog transfer and the
  API for ongoing real-time maintenance.
- Custom product fields are supported but must be configured with Optoro's Client Success team first.
