# Optoro

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Optoro is a returns management and reverse-logistics software company (Washington, DC; acquired by Blue Yonder in August 2025) whose OptiTurn platform powers the full returns lifecycle for retailers, brands and 3PLs — a shopper-facing returns portal and RMA workflow, in-store and warehouse returns processing, disposition and routing decisions, drop-ship fulfillment of returned and excess inventory, return-to-vendor agreements, and resale across secondary channels. Optoro publishes a public, API-first developer portal at developer.optoro.com covering seventeen OpenAPI 3.0/3.1 definitions across two directions: inbound APIs the retailer calls (Catalogs, Facilities, Drop Ship, RTV Vendor, ASN, External Bin Changes, Auth) and outbound webhooks/customer endpoints Optoro calls (RMAs, Disposition Update, Final Disposition, Outbound ASN, Exchange Orders, Exchange Variants, Drop Ship confirmation/cancellation). Authentication is OAuth 2.0 client credentials against auth.optiturn.com with 25-hour bearer tokens, and a full sandbox estate is published on *.sandbox.optiturn.com.

**Areas:** Returns Management · Reverse Logistics · Retail · Supply Chain · E-Commerce · Fulfillment · Dropship · Inventory · Webhook · Order Management

## Optoro on APIs.io

Everything profiled for Optoro is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/optoro/](https://apis.io/providers/optoro/)** — or go straight to one of the APIs or properties below.

### APIs (21)

- [Optoro Catalog Entry Updates API](https://apis.io/apis/optoro/optoro-catalog-entry-updates-api/) — The Catalog Entry Updates API from Optoro — 1 operation(s) for catalog entry updates.
- [Optoro Dispositions API](https://apis.io/apis/optoro/optoro-dispositions-api/) — The Dispositions API from Optoro — 1 operation(s) for dispositions.
- [Optoro Drop Shipment Cancellation API](https://apis.io/apis/optoro/optoro-drop-shipment-cancellation-api/) — The Drop Shipment Cancellation API from Optoro — 1 operation(s) for drop shipment cancellation.
- [Optoro Drop Shipment Confirmation API](https://apis.io/apis/optoro/optoro-drop-shipment-confirmation-api/) — The Drop Shipment Confirmation API from Optoro — 1 operation(s) for drop shipment confirmation.
- [Optoro Drop Shipment Partial Cancellation API](https://apis.io/apis/optoro/optoro-drop-shipment-partial-cancellation-api/) — The Drop Shipment Partial Cancellation API from Optoro — 1 operation(s) for drop shipment partial cancellation.
- [Optoro Exchange Orders API](https://apis.io/apis/optoro/optoro-exchange-orders-api/) — The Exchange Orders API from Optoro — 1 operation(s) for exchange orders.
- [Optoro External Bin Changes API](https://apis.io/apis/optoro/optoro-external-bin-changes-api/) — The External Bin Changes API from Optoro — 2 operation(s) for external bin changes.
- [Optoro Facilities API](https://apis.io/apis/optoro/optoro-facilities-api/) — The Facilities API from Optoro — 1 operation(s) for facilities.
- [Optoro Final Dispositions API](https://apis.io/apis/optoro/optoro-final-dispositions-api/) — The Final Dispositions API from Optoro — 1 operation(s) for final dispositions.
- [Optoro Forward Orders API](https://apis.io/apis/optoro/optoro-forward-orders-api/) — The Forward Orders API from Optoro — 1 operation(s) for forward orders.
- [Optoro Inventory Receipt API](https://apis.io/apis/optoro/optoro-inventory-receipt-api/) — The Inventory Receipt API from Optoro — 1 operation(s) for inventory receipt.
- [Optoro Listings API](https://apis.io/apis/optoro/optoro-listings-api/) — The Listings API from Optoro — 2 operation(s) for listings.
- [Optoro Orders API](https://apis.io/apis/optoro/optoro-orders-api/) — The Orders API from Optoro — 3 operation(s) for orders.
- [Optoro Outbound Asn API](https://apis.io/apis/optoro/optoro-outbound-asn-api/) — The Outbound Asn API from Optoro — 1 operation(s) for outbound asn.
- [Optoro Returns Portal Orders API](https://apis.io/apis/optoro/optoro-returns-portal-orders-api/) — The Returns Portal Orders API from Optoro — 1 operation(s) for returns portal orders.
- [Optoro Rmas API](https://apis.io/apis/optoro/optoro-rmas-api/) — The Rmas API from Optoro — 1 operation(s) for rmas.
- [Optoro Shipments API](https://apis.io/apis/optoro/optoro-shipments-api/) — The Shipments API from Optoro — 3 operation(s) for shipments.
- [Optoro Sku API](https://apis.io/apis/optoro/optoro-sku-api/) — The Sku API from Optoro — 1 operation(s) for sku.
- [Optoro Vendor Updates API](https://apis.io/apis/optoro/optoro-vendor-updates-api/) — The Vendor Updates API from Optoro — 1 operation(s) for vendor updates.
- [Optoro Asns API](https://apis.io/apis/optoro/optoro-asns-api/) — The Asns API from Optoro — 2 operation(s) for asns.
- [Optoro OAUTH API](https://apis.io/apis/optoro/optoro-oauth-api/) — The Oauth API from Optoro — 1 operation(s) for oauth.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Optoro Webhooks](https://apis.io/asyncapis/optoro/optoro-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [optoro](https://apis.io/servers/optoro/optoro/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Optoro Agentic Access](https://apis.io/agentic-access/optoro/optoro-agentic-access/)

#### Overlays (17)

OpenAPI overlays, including conversational phrasing for each operation.

- [Optoro Asn Overlay](https://apis.io/overlays/optoro/optoro-asn-overlay/)
- [Optoro Auth Overlay](https://apis.io/overlays/optoro/optoro-auth-overlay/)
- [Optoro Catalogs Overlay](https://apis.io/overlays/optoro/optoro-catalogs-overlay/)
- [Optoro Disposition Update Overlay](https://apis.io/overlays/optoro/optoro-disposition-update-overlay/)
- [Optoro Drop Ship Overlay](https://apis.io/overlays/optoro/optoro-drop-ship-overlay/)
- [Optoro Drop Ship Webhooks Overlay](https://apis.io/overlays/optoro/optoro-drop-ship-webhooks-overlay/)
- [Optoro Exchange Orders Overlay](https://apis.io/overlays/optoro/optoro-exchange-orders-overlay/)
- [Optoro External Bin Changes Overlay](https://apis.io/overlays/optoro/optoro-external-bin-changes-overlay/)
- [Optoro Facilities Overlay](https://apis.io/overlays/optoro/optoro-facilities-overlay/)
- [Optoro Final Disposition Overlay](https://apis.io/overlays/optoro/optoro-final-disposition-overlay/)
- [Optoro Forward Orders Overlay](https://apis.io/overlays/optoro/optoro-forward-orders-overlay/)
- [Optoro Inventory Receipt Overlay](https://apis.io/overlays/optoro/optoro-inventory-receipt-overlay/)
- [Optoro Outbound Asn Overlay](https://apis.io/overlays/optoro/optoro-outbound-asn-overlay/)
- [Optoro Returns Portal Orders Overlay](https://apis.io/overlays/optoro/optoro-returns-portal-orders-overlay/)
- [Optoro Rmas Overlay](https://apis.io/overlays/optoro/optoro-rmas-overlay/)
- [Optoro Rtv Overlay](https://apis.io/overlays/optoro/optoro-rtv-overlay/)
- [Optoro Variants Overlay](https://apis.io/overlays/optoro/optoro-variants-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Optoro Authentication](https://apis.io/security/optoro/optoro-authentication/)
- [Optoro Domain Security](https://apis.io/security/optoro/optoro-domain-security/)
- [Optoro Vulnerability Disclosure](https://apis.io/security/optoro/optoro-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Optoro Scopes](https://apis.io/scopes/optoro/optoro-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Optoro Plans Pricing](https://apis.io/plans/optoro/optoro-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Optoro Rate Limits](https://apis.io/rate-limits/optoro/optoro-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.optoro.com/)
- [Documentation](https://developer.optoro.com/content/api_overview)
- [Getting started](https://developer.optoro.com/content/rx_integration_guide)
- [API reference](https://developer.optoro.com/openapi/rmas/openapi)
- [Support](https://help.optoro.com/hc/en-us)
- [Blog](https://www.optoro.com/returns-blog/)
- [Security](https://www.optoro.com/security/)
- [Compliance](https://www.optoro.com/security/)
- [Trust centre](https://www.optoro.com/security/)
- [Terms of service](https://www.optoro.com/terms-conditions/)
- [Privacy policy](https://www.optoro.com/privacy-policy/)
- [GitHub](https://github.com/optoro)
- [Status](https://status.optiturn.com/)

## API Evangelist rating

**Kin Score 61.9** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 56.7 |
| Contract governance | 18.2 |
| Operational transparency | 73.7 |
| Developer ergonomics | 61.3 |
| Access clarity | 43.4 |

**Agent readiness 33.9** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 45.1** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/optoro/](https://apis.io/providers/optoro/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Optoro: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/optoro/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
