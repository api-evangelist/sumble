---
name: Enrich and search organizations
description: Resolve companies you already have (by domain) or search Sumble's database by technology, job function, and firmographics, composing exactly the attributes and metrics you need.
api: openapi/sumble-openapi-original.json
operations:
  - enrich_organizations_unified__api_version__organizations_post
  - get_organization_signals__api_version__organizations__organization_id__signals_get
---

# Enrich and search organizations

Use Sumble's single composable `/v9/organizations` endpoint to either resolve a
list of companies you already have or search by advanced filters.

## Auth
- Header: `Authorization: Bearer YOUR_API_KEY` (generate at https://sumble.com/account/api-keys).
- Base URL: `https://api.sumble.com`.

## Steps
1. **Resolve or search** — `POST /v9/organizations`
   (`enrich_organizations_unified__api_version__organizations_post`).
   - Resolve mode: pass `organizations: [ { "url": "stripe.com" } ]`.
   - Search mode: pass an advanced filter (technology, job function, industry, firmographics).
   - Use the `select` block to choose exactly which attributes and per-entity
     metrics return — this drives credit cost.
   - Paginate with `limit` and `offset`; read `total` from the response.
2. **Pull recent signals** for a resolved org — `GET /v9/organizations/{organization_id}/signals`
   (`get_organization_signals__api_version__organizations__organization_id__signals_get`).

## Rules
- Rate limit: 10 requests/second per user (aggregated); back off on `429`.
- `402` means insufficient credits — narrow your `select` or top up.
- `422` is a validation error; fix the fields listed in `detail[].loc`.
- See conventions/sumble-conventions.yml and errors/sumble-problem-types.yml.
