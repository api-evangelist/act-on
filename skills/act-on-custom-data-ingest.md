---
name: act-on-custom-data-ingest
description: Define an Act-On Custom Data schema, create a dataset, validate and ingest records, poll the job, and query the data joined against Act-On Contacts.
api: Act-On Custom Objects Service
base_url: https://api.actonsoftware.com/custom-objects
spec: openapi/act-on-custom-objects-service-openapi.yml
operations:
  - getAllSchemas
  - createSchema
  - getSchema
  - updateSchema
  - addFields
  - updateFields
  - deleteFields
  - createDataset
  - describeDataset
  - listDatasetsBySchemaId
  - listAllDatasets
  - validateFile
  - ingestFile
  - ingestJsonStream
  - getJobStatus
  - getJobReport
  - queryData
  - deleteIds
generated: '2026-08-13'
method: generated
source: openapi/act-on-custom-objects-service-openapi.yml (operationIds verified against the published contract)
---

# Ingest and query Act-On Custom Data

**Access first: this surface is in BETA and request-only.** Act-On's own overview
page states the Custom Data endpoints "are currently in BETA and are only available on
request" and points at an enrolment form
(<https://developer.act-on.com/reference/overview>). If your account is not enrolled,
no amount of correct request-shaping will help.

This is the best-specified corner of Act-On's API — the only document with named
component schemas (12 DTOs), the only one with cursor pagination, and the only one
with an explicit join.

Base path: `https://api.actonsoftware.com/custom-objects`, versioned `/v1`, every
operation scoped by `{accountId}`. Auth is `Authorization: Bearer <token>` (declared
as `http`/`bearer`, `bearerFormat: JWT`).

## Steps

### 1. Schema
- `getAllSchemas` — see what already exists before creating anything.
- `createSchema` (`POST /v1/{accountId}/schema`) with a `CreateSchemaRequestDTO`:
  `name`, `description`, `dataType`, `fields[]` (`FieldDefinitionDTO`),
  `requiredFields[]`, `uniqueFieldSet[]`, `eventTimestampField`.
- `getSchema` / `updateSchema` to read and amend basic properties.
- Field-level changes: `addFields`, `updateFields`, `deleteFields`.
  Field `properties` are type-dependent — `format` (`json|base64`) for JSON,
  `enumName`/`enumValues`/`enumValuesCaseSensitive` for ENUM, `CSVSeparator`
  (comma, semicolon, pipe, tab) for STRING_ARRAY, a date format for DATE.

`uniqueFieldSet` is the one to get right first: it determines what counts as the same
record on re-ingest.

### 2. Dataset
- `createDataset` (`POST /v1/{accountId}/data/{objectId}`) — an empty dataset for the
  schema.
- `describeDataset`, `listDatasetsBySchemaId`, `listAllDatasets` to find existing ones.

### 3. Validate, then ingest
- **`validateFile` first.** It checks a file against the schema *without* ingesting.
  Use it every time; it is the closest thing this API has to a dry run.
- `ingestFile` (CSV or JSON upload) or `ingestJsonStream` (JSON stream).
- Both are asynchronous and return a job id.

### 4. Poll the job
- `getJobStatus` (`GET /v1/{accountId}/data/status/{jobId}`).
- On failure `getJobReport` returns the report for a completed job — read it before
  re-ingesting, or you will repeat the same rejection.
- There is **no webhook** on job completion. Poll with backoff; Act-On's account-wide
  ceiling is 5 requests/second and 30,000/day.

### 5. Query
`queryData` (`POST /v1/{accountId}/query/{objectId}/{datasetId}/joinWithOther`) takes
a `DataQueryRequestDTO`:

- `selectFields[]` — **prefix every field**: `aoc.` for Act-On Contacts fields, `co.`
  for custom-object fields. `aoc.*` / `co.*` select all. Max 2000 entries.
- `pagination` (`PaginationDTO`) — `pageStrategy` is `OFFSET` (default) or `CURSOR`;
  cursor pages carry `nextPageToken`. **Use the `pagination` object, not the flat
  `page`/`size` body fields** — those are marked deprecated in Act-On's own schema.
- `sort[]` (`SortFieldDTO`) — `field` (same `aoc.`/`co.` prefixes) plus
  `direction: asc|desc`.
- `joinStrategy` (`JoinStrategyDTO`) — `useDefaults` picks the right behaviour from
  the object's relationship type (one-to-one vs one-to-many) and ignores everything
  else. Prefer it unless you know exactly why you are overriding `duplicates`,
  `onlyMatching` and `joinEnabled`.

## Deleting

`deleteIds` removes records by id or id range. `deleteSchema` and the
delete-all-schemas operation destroy definitions and everything under them. All are
irreversible and none is idempotency-protected. Confirm with a human.

## Errors

This service uses the Spring-style envelope, not the `/api/1` numeric one:
`{errorId, requestUri, errorMessage, errorList[], status}` where `status` is a string
like `"400 BAD_REQUEST"`. `errorList[]` carries per-field validation messages — read
it, it is the most useful error detail anywhere in Act-On's API.

See `errors/act-on-problem-types.yml` and `data-model/act-on-data-model.yml`.
