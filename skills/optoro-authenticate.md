---
name: optoro-authenticate
description: Obtain and reuse an Optoro OAuth 2.0 client-credentials access token for any Optoro API.
api: Optoro Auth API
operations:
  - oauthTokenFetch
source: https://developer.optoro.com/content/api_overview
generated: '2026-08-26'
method: generated
---

# Authenticate with Optoro

Every Optoro API is authorized by one bearer token. There is no per-API credential and no self-serve key
generation — Optoro's Client Success team issues the `client_id` and `client_secret`.

## Steps

1. **Fetch a token.** `POST https://auth.optiturn.com/oauth/token` (`oauthTokenFetch`,
   `openapi/optoro-auth-openapi.yml`) with `Content-Type: application/json` and a body of
   `{"grant_type": "client_credentials", "client_id": "...", "client_secret": "..."}`.
   In sandbox use `https://auth.sandbox.optiturn.com/oauth/token`.
2. **Read the response.** It returns `access_token`, `token_type` (`Bearer`), `expires_in` (`90000`
   seconds = 25 hours), `scope` (`read write`) and `created_at`.
3. **Cache the token for 25 hours.** Optoro states explicitly: "Access tokens are valid for 25 hours and
   should be reused. There is no need to request a new token until the previous token expires. The same
   token may be used across all of Optoro's APIs." Do not mint a token per request.
4. **Send it.** `Authorization: bearer {access_token}`, plus `Content-Type: application/json` and
   `Accept: application/json`. Some APIs also require a version header, e.g.
   `X-Optiturn-Api-Version: 1` — read the individual spec, the name and value vary.

## Failure handling

- `401` — token missing or expired. Re-run step 1 once, then retry the original call.
- `400` — malformed token request body.
- `422` — validation failure on the token request; read `errors[].field` and `errors[].code`.
- `5XX` — retry up to three times with exponential backoff.

## Constraints

- TLS 1.2 or higher only. Google Trust Services and Let's Encrypt roots must be installed.
- Production is limited to 5000 requests per minute per IP, sandbox to 2500. Exhaustion returns `429`
  with **no** `Retry-After` header — back off exponentially.
