---
name: Find companies using a technology
description: Look up a technology by name to get its canonical id, then search organizations that use it and compose the firmographics and metrics you need for targeting.
api: openapi/sumble-openapi-original.json
operations:
  - get_technologies__api_version__technologies_find_post
  - lookup_technologies__api_version__technologies_lookup_post
  - enrich_organizations_unified__api_version__organizations_post
---

# Find companies using a technology

## Auth
- `Authorization: Bearer YOUR_API_KEY`; base URL `https://api.sumble.com`.

## Steps
1. **Find the technology** — `POST /v9/technologies/find`
   (`get_technologies__api_version__technologies_find_post`) to search technologies
   by name, or `POST /v9/technologies/lookup`
   (`lookup_technologies__api_version__technologies_lookup_post`) to resolve known
   slugs/ids to canonical technology entities.
2. **Search organizations by that technology** — `POST /v9/organizations`
   (`enrich_organizations_unified__api_version__organizations_post`) in search mode,
   filtering on the technology id from step 1. Use `select` to compose firmographics
   and per-technology metrics.

## Rules
- Technology lookups cost ~1 credit per 100 matched technologies; a
  `technology_category` with `granularity: "exploded"` multiplies metric cost by
  the number of technologies in the category.
- Rate limit 10 req/s → `429`; insufficient credits → `402`.
- See conventions/sumble-conventions.yml for pagination (`limit`/`offset`/`total`).
