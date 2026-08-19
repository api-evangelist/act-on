---
name: act-on-import-contacts
description: Bulk-import contacts into Act-On Contacts by creating (or reusing) an import definition, posting the file, and polling the import job to completion.
api: Act-On REST API
base_url: https://api.actonsoftware.com
spec: openapi/act-on-rest-api-openapi.yml
operations:
  - get-import-definitions
  - create-an-import-definition
  - get-import-definition-by-id
  - update-an-import-definition
  - import-contacts
  - get-import-status
generated: '2026-08-13'
method: generated
source: openapi/act-on-rest-api-openapi.yml (operationIds verified against the published contract)
---

# Import contacts into Act-On

Act-On's bulk contact import is a two-object flow: an **import definition** describes
how a file maps onto the Act-On Contacts schema, and an **import job** runs a file
through it. The definition is reusable; create it once and reuse it every run.

Every operation in this skill lives under `/ucl/v2/{accountId}/...`, so you need the
**account id** in session state. The access token alone is not enough — unlike the
`/api/1` surface, the UCL surface will not infer the account for you.

## Before you start

- Authenticate first. `POST /token` with the `password` grant returns an
  `access_token` and a `refresh_token`. Send `Authorization: Bearer <access_token>`.
- **Cache the token.** Act-On allows only **5 authentication calls per hour**. Refresh
  on expiry, never per request.
- Budget the run against **5 requests/second** and **30,000 requests/day**.

## Steps

1. **Find an existing definition.** `get-import-definitions`
   (`GET /ucl/v2/{accountId}/import/definition`). Reuse a definition whose field
   mapping already matches your file rather than creating a near-duplicate.
2. **Create one if none fits.** `create-an-import-definition`
   (`POST /ucl/v2/{accountId}/import/definition`). Keep the returned
   `importDefinitionId`.
3. **Confirm the mapping.** `get-import-definition-by-id`
   (`GET /ucl/v2/{accountId}/import/definition/{importDefinitionId}`). If the source
   file has changed shape, `update-an-import-definition`
   (`PUT .../{importDefinitionId}`) rather than creating another one.
4. **Post the file.** `import-contacts`
   (`POST /ucl/v2/{accountId}/import/contacts/{importDefinitionId}`). Keep the
   returned import id.
5. **Poll to completion.** `get-import-status`
   (`GET /ucl/v2/{accountId}/import/status/{importId}`). There is **no webhook** on
   job completion, so polling is the only option. Back off — a tight poll loop will
   spend the 5/second budget on nothing.

## Failure handling

`/ucl/v2` errors are the thin ones. Several statuses are declared as `text/plain`
with an **empty body**, so the status code is your only diagnostic:

| Status | What it means here | Action |
|---|---|---|
| 401 | Token missing, expired or wrong account | Refresh; do not retry blind (5 auth calls/hour) |
| 403 | Account lacks permission for this definition | Stop; a human has to fix permissions |
| 406 / 415 | Wrong `Content-Type` or unacceptable file | Fix the request, do not retry as-is |
| 409 | Conflicting import already running | Wait for the in-flight job, then retry |
| 413 | File too large | Split it. Docs publish a 400MB ceiling; this operation's own 413 example says "File size exceeds the maximum limit of 200MB." Assume the smaller number |
| 500 | Server-side | Safe to retry with backoff — an import that failed did not partially commit contacts under a new definition, but verify with `get-import-status` before re-posting |

## Do not

- **Do not retry a successful-looking POST.** There is no `Idempotency-Key` anywhere
  in Act-On's contract. A re-posted import is a second import.
- **Do not invent the account id.** It is a required path parameter; get it from the
  operator, not from the token.

See `conventions/act-on-conventions.yml`, `errors/act-on-problem-types.yml` and
`rate-limits/act-on-rate-limits.yml`.
