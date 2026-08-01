---
name: Build an account list and arm it with signals
description: Create an organization list, add target companies to it, and configure the buying/hiring signals Sumble should track for that list.
api: openapi/sumble-openapi-original.json
operations:
  - create_organization_list__api_version__organization_lists_post
  - add_organizations_to_list__api_version__organization_lists__list_id__organizations_post
  - set_organization_list_signals__api_version__organization_lists__list_id__signals_post
  - get_organization_list__api_version__organization_lists__list_id__get
---

# Build an account list and arm it with signals

## Auth
- `Authorization: Bearer YOUR_API_KEY`; base URL `https://api.sumble.com`.

## Steps
1. **Create the list** — `POST /v9/organization-lists`
   (`create_organization_list__api_version__organization_lists_post`). Capture the
   returned `list_id`.
2. **Add organizations** — `POST /v9/organization-lists/{list_id}/organizations`
   (`add_organizations_to_list__api_version__organization_lists__list_id__organizations_post`)
   with the organization ids you want to track.
3. **Configure signals** — `POST /v9/organization-lists/{list_id}/signals`
   (`set_organization_list_signals__api_version__organization_lists__list_id__signals_post`)
   to arm the list with the hiring/buying signals Sumble should surface.
4. **Read back the list** — `GET /v9/organization-lists/{list_id}`
   (`get_organization_list__api_version__organization_lists__list_id__get`).

## Rules
- Rate limit 10 req/s → `429`; `422` validation errors list offending fields in
  `detail[].loc`.
- No idempotency-key contract: guard against duplicate list/member creation
  client-side. See conventions/sumble-conventions.yml.
