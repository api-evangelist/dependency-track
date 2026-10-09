---
generated: '2026-10-09'
method: generated
name: export-sbom-and-vex
description: Export a project as a CycloneDX SBOM and as CycloneDX VEX, or import VEX analysis decisions.
api: openapi/dependency-track-openapi.yml
operations:
- exportProjectAsCycloneDx
- exportProjectAsCycloneDx_1
- uploadVex
source: 'Grounded in openapi/dependency-track-openapi.yml; operationIds verified verbatim. Auth: X-Api-Key header or Bearer
  session token (spec securitySchemes). Errors: 401 missing/invalid credentials, 403 missing permission or project access,
  504 timeout (info.description).'
---

# Export a project as a CycloneDX SBOM and as CycloneDX VEX, or import VEX analysis decisions.

## Steps

1. Export the SBOM with `exportProjectAsCycloneDx` (GET /v1/bom/cyclonedx/project/{uuid}).
2. Export VEX with `exportProjectAsCycloneDx_1` (GET /v1/vex/cyclonedx/project/{uuid}).
3. Import VEX decisions with `uploadVex` (PUT /v1/vex).

## Rules

- Base URL is your own self-hosted instance (`<host>/api`); there is no vendor-hosted API.
- v1: PUT creates, POST updates. Watch for the `X-API-Deprecated: true` response header.
- No idempotency keys are documented; re-check state before retrying writes.
