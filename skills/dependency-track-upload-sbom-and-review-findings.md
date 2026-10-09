---
generated: '2026-10-09'
method: generated
name: upload-sbom-and-review-findings
description: Upload a CycloneDX SBOM to a Dependency-Track project, wait for analysis, and read the resulting findings and
  metrics.
api: openapi/dependency-track-openapi.yml
operations:
- getProjectByNameAndVersion
- UploadBom
- isTokenBeingProcessed_1
- getFindingsByProject
- getProjectCurrentMetrics
source: 'Grounded in openapi/dependency-track-openapi.yml; operationIds verified verbatim. Auth: X-Api-Key header or Bearer
  session token (spec securitySchemes). Errors: 401 missing/invalid credentials, 403 missing permission or project access,
  504 timeout (info.description).'
---

# Upload a CycloneDX SBOM to a Dependency-Track project, wait for analysis, and read the resulting findings and metrics.

## Steps

1. Resolve the project with `getProjectByNameAndVersion` (GET /v1/project/lookup); or let `UploadBom` create it with `autoCreate=true` plus `projectName`/`projectVersion` (needs PORTFOLIO_MANAGEMENT, PORTFOLIO_MANAGEMENT_CREATE or PROJECT_CREATION_UPLOAD per the operation description).
2. POST the BOM as multipart/form-data with `UploadBom` (POST /v1/bom). Keep the returned token.
3. Poll `isTokenBeingProcessed_1` (GET /v1/event/token/{uuid}) until processing is false. The older GET /v1/bom/token/{uuid} is deprecated.
4. Read findings with `getFindingsByProject` (GET /v1/finding/project/{uuid}).
5. Read risk totals with `getProjectCurrentMetrics` (GET /v1/metrics/project/{uuid}/current).

## Rules

- Base URL is your own self-hosted instance (`<host>/api`); there is no vendor-hosted API.
- v1: PUT creates, POST updates. Watch for the `X-API-Deprecated: true` response header.
- No idempotency keys are documented; re-check state before retrying writes.
