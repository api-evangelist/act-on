---
name: act-on-build-segment
description: Build and maintain an Act-On audience segment — create it, add or remove contacts by id, email or external id, and read its membership.
api: Act-On REST API
base_url: https://api.actonsoftware.com
spec: openapi/act-on-rest-api-openapi.yml
operations:
  - get-segments
  - create-a-segment
  - get-segment-by-id
  - update-segment-if-its-a-direct-select-segment-only-the-name-can-be-updated
  - get-contacts-from-a-segment
  - add-contacts-to-a-direct-select-segment
  - add-contacts-to-a-direct-select-segment-by-external-id
  - remove-contacts-from-direct-select-segment
  - remove-contacts-from-direct-select-segment-by-email
  - remove-contacts-from-direct-select-segment-by-external-id
  - delete-segment
  - get-all-segments-that-the-contact-belong-by-id
generated: '2026-08-13'
method: generated
source: openapi/act-on-rest-api-openapi.yml (operationIds verified against the published contract)
---

# Build an Act-On segment

Everything here is on the `/ucl/v2/{accountId}/segment/...` surface, so the **account
id is a required path parameter** on every call.

## The one thing that decides the whole flow

Act-On has two kinds of segment, and only one of them accepts explicit membership
writes:

- **Direct Select** — you name the members. All the add/remove operations below apply.
- **Rule-based** — Act-On computes membership from criteria. You may read it; you may
  not write members into it, and `update-segment-...` will only let you change the
  **name**. The operationId says so out loud:
  `update-segment-if-its-a-direct-select-segment-only-the-name-can-be-updated`.

Establish which kind you are holding *before* you attempt a membership write.

## Steps

1. **List segments.** `get-segments` (`GET /ucl/v2/{accountId}/segment/`). Supports
   `page` + `pageSize` — note this surface pages differently from `/api/1`, which uses
   `offset` + `count`.
2. **Create.** `create-a-segment` (`POST /ucl/v2/{accountId}/segment/`). Keep the
   `segmentId`.
3. **Inspect.** `get-segment-by-id` (`GET .../segment/{segmentId}`).
4. **Add members** (Direct Select only):
   - by internal id — `add-contacts-to-a-direct-select-segment`
     (`PUT .../segment/{segmentId}/contacts`)
   - by external id — `add-contacts-to-a-direct-select-segment-by-external-id`
     (`PUT .../segment/{segmentId}/externalId/contacts`)
5. **Remove members** (Direct Select only):
   - by internal id — `remove-contacts-from-direct-select-segment`
     (`DELETE .../segment/{segmentId}/contacts`)
   - by email — `remove-contacts-from-direct-select-segment-by-email`
     (`DELETE .../segment/{segmentId}/email/contact`)
   - by external id — `remove-contacts-from-direct-select-segment-by-external-id`
     (`DELETE .../segment/{segmentId}/externalId/contacts`)
6. **Read membership.** `get-contacts-from-a-segment`
   (`GET .../segment/{segmentId}/contacts`).
7. **Check from the contact side.**
   `get-all-segments-that-the-contact-belong-by-id`
   (`GET /ucl/v2/{accountId}/contactReport/id/{id}/segments`) — useful for verifying a
   write landed without pulling the whole segment.

## Deleting

`delete-segment` (`DELETE .../segment/{segmentId}`) has **no documented soft delete
and no undo**. Confirm with a human, and read the membership first if it matters.

## Errors

`/ucl/v2` returns `text/plain` with an **empty body** on 401, 403, 404, 406, 409, 415
and 500 — the status code is all you get. A `409` on a membership write usually means
a concurrent write against the same segment; wait and retry. Do not retry a 4xx
unchanged.

There is no idempotency key, but the membership operations are set-semantics: adding a
contact that is already a member is not a second membership. The delete operations are
likewise safe to repeat.

See `conventions/act-on-conventions.yml` and `data-model/act-on-data-model.yml`.
