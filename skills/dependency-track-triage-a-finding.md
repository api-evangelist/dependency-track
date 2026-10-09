---
generated: '2026-10-09'
method: generated
name: triage-a-finding
description: Record an analysis decision (state, justification, suppression) for a vulnerability on a component.
api: openapi/dependency-track-openapi.yml
operations:
- getFindingsByProject
- retrieveAnalysis
- updateAnalysis
source: 'Grounded in openapi/dependency-track-openapi.yml; operationIds verified verbatim. Auth: X-Api-Key header or Bearer
  session token (spec securitySchemes). Errors: 401 missing/invalid credentials, 403 missing permission or project access,
  504 timeout (info.description).'
---

# Record an analysis decision (state, justification, suppression) for a vulnerability on a component.

## Steps

1. List findings with `getFindingsByProject` to get the component and vulnerability UUIDs.
2. Read the current decision with `retrieveAnalysis` (GET /v1/analysis).
3. Write the decision with `updateAnalysis` (PUT /v1/analysis). Requires VULNERABILITY_ANALYSIS or VULNERABILITY_ANALYSIS_UPDATE.

## Rules

- Base URL is your own self-hosted instance (`<host>/api`); there is no vendor-hosted API.
- v1: PUT creates, POST updates. Watch for the `X-API-Deprecated: true` response header.
- No idempotency keys are documented; re-check state before retrying writes.
