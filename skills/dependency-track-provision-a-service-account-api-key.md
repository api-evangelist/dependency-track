---
generated: '2026-10-09'
method: generated
name: provision-a-service-account-api-key
description: Create a v2 service account and issue it an API key for machine-to-machine access.
api: openapi/dependency-track-v2-openapi.yml
operations:
- createServiceAccount
- createServiceAccountApiKey
- listServiceAccountApiKeys
source: 'Grounded in openapi/dependency-track-v2-openapi.yml; operationIds verified verbatim. Auth: X-Api-Key header or Bearer
  session token (spec securitySchemes). Errors: 401 missing/invalid credentials, 403 missing permission or project access,
  504 timeout (info.description).'
---

# Create a v2 service account and issue it an API key for machine-to-machine access.

## Steps

1. Create the account with `createServiceAccount` (POST /api/v2/service-accounts).
2. Issue a key with `createServiceAccountApiKey` (POST /api/v2/service-accounts/{name}/api-keys); send it later as the X-Api-Key header.
3. Audit keys with `listServiceAccountApiKeys`; v2 collections use token-based pagination (next_page_token).

## Rules

- Base URL is your own self-hosted instance (`<host>/api`); there is no vendor-hosted API.
- v1: PUT creates, POST updates. Watch for the `X-API-Deprecated: true` response header.
- No idempotency keys are documented; re-check state before retrying writes.
