---
name: act-on-send-email-campaign
description: Create a draft or template message in Act-On, send it, and pull the resulting message report — with the guard rails an irreversible send requires.
api: Act-On REST API
base_url: https://api.actonsoftware.com
spec: openapi/act-on-rest-api-openapi.yml
operations:
  - get-message-list
  - add-new-template-or-draft-message
  - update-template-or-draft-message
  - get-message-html-contents
  - send-a-message
  - resend-a-message
  - get-message-report
  - get-message-report-drilldown
  - get-message-report-by-time-period
  - delete-a-message
generated: '2026-08-13'
method: generated
source: openapi/act-on-rest-api-openapi.yml (operationIds verified against the published contract)
---

# Send an email campaign with Act-On

This skill puts mail in real inboxes. Read the guard rails before the steps.

## Guard rails — read first

- **The send is irreversible and externally visible.** `send-a-message` has no
  preview mode, no dry run and no scheduled-cancel operation in the published
  contract.
- **There is no idempotency key.** Act-On documents none on any of its 158
  operations. If `POST /api/1/message/{msgid}/send` times out, you **cannot** safely
  retry it — a retry is a second send to the same audience. Poll
  `get-message-report` to find out whether the first one landed, then decide.
- **Never send without an explicit human confirmation** naming the message and the
  audience.

## Steps

1. **Find or create the message.**
   - List what exists: `get-message-list` (`GET /api/1/message`). Supports
     `offset` + `count`; the response envelope is
     `{offset, count, totalCount, ...}`.
   - Create a draft or template: `add-new-template-or-draft-message`
     (`POST /api/1/message`). Note this is the `/api/1` surface — bodies are
     **form-encoded**, not JSON.
   - Amend it: `update-template-or-draft-message` (`PUT /api/1/message/{id}`).
2. **Verify the rendered content** before you send:
   `get-message-html-contents` (`GET /api/1/message/{id}/{recid}`). Show the operator
   what will actually go out.
3. **Confirm the audience.** The recipient list/segment is bound to the message in
   Act-On, not passed on the send call — so verify it out of band with
   `get-list-of-act-on-assets` or `get-segments` before step 4.
4. **Send.** `send-a-message` (`POST /api/1/message/{msgid}/send`). One call. Record
   the message id and the wall-clock time immediately.
5. **Report.**
   - Per-message: `get-message-report` (`GET /api/1/message/{id}/report`).
   - Drill into a behaviour: `get-message-report-drilldown`
     (`GET /api/1/message/{id}/report/{drilldown}`) — supports `offset` + `count`.
     An invalid verb returns `errorCode` **10089** ("Invalid drill-down verb").
   - Across a window: `get-message-report-by-time-period`
     (`GET /api/1/message/report`). A bad range returns `errorCode` **10160**
     ("The date period is invalid.").

## Resending

`resend-a-message` (`PUT /api/1/message/{msgid}/send`) is a **deliberate second
send**, not a retry primitive. Only call it when a human has asked for a resend.

## Errors you will actually hit

- `404` with `errorCode` **10030** — "Invalid or deleted message". The message id is
  stale.
- Gateway `401` — `{"httpCode":"401","httpMessage":"Unauthorized"}`. Refresh the
  token; remember the 5-auth-calls-per-hour ceiling.
- Transactional email (`POST /ete/v1/email/{accountid}/{templateid}`) returns `500`
  with `{"errorName":"EmailServiceException","message":"A transactional subscription
  is required..."}` when the account has no transactional subscription. **That is not
  retryable** — it is an entitlement problem.

See `errors/act-on-problem-types.yml` for the full numeric error-code table.
