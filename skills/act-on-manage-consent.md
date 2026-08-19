---
name: act-on-manage-consent
description: Read and write Act-On subscription categories, opt-outs and suppression lists — the consent surface, where getting it wrong is a compliance event rather than a bug.
api: Act-On REST API
base_url: https://api.actonsoftware.com
spec: openapi/act-on-rest-api-openapi.yml
operations:
  - get-subscription-categories
  - set-multiple-subscriptions-by-email-address
  - update-subscription-by-email
  - get-subscription-opt-outs-by-category
  - get-opt-out-list
  - update-optout-list
  - remove-opt-outs-1
  - get-hard-bounce-list
  - get-spam-complaint-list
generated: '2026-08-13'
method: generated
source: openapi/act-on-rest-api-openapi.yml (operationIds verified against the published contract)
---

# Manage consent and suppression in Act-On

These operations write **consent state**. Treat every one of them as requiring an
explicit, recorded human instruction. An agent that opts someone back in on its own
initiative has created a legal problem, not a data problem.

## Read before you write

1. **What categories exist?** `get-subscription-categories`
   (`GET /api/1/subscription/category`). Categories are account-defined; never assume
   a name.
2. **Who has opted out of a category?** `get-subscription-opt-outs-by-category`
   (`GET /api/1/subscription/optout`).
3. **Account-wide opt-out list.** `get-opt-out-list` (`GET /api/1/list/optout`).
4. **Deliverability suppression.** `get-hard-bounce-list`
   (`GET /api/1/list/hardbounce`) and `get-spam-complaint-list`
   (`GET /api/1/list/spamcomplaint`). These are *not* consent — they are delivery
   failures and complaints — but sending to them is how a sender reputation dies.

## Writes

- **Set a contact's categories:** `set-multiple-subscriptions-by-email-address`
  (`PUT /api/1/subscription/setcategories`). This sets the full category state for
  the address in one call — read the current state first, or you will silently clear
  categories you did not intend to touch.
- **Opt a contact out:** `update-subscription-by-email`
  (`PUT /api/1/subscription/optout`).
- **Modify the account opt-out list:** `update-optout-list`
  (`PUT /api/1/list/optout`).
- **Opt records back in:** `remove-opt-outs-1` (`PUT /api/1/list/optin`).

### The rule for opt-in

**Never call `remove-opt-outs-1` (opt-in) speculatively.** Opting a contact back in
reverses a choice they made. Require, and record, a specific human instruction naming
the addresses. Opting *out* on a contact's request is always safe; opting *in* never
is.

## Mechanics

- These are `/api/1` operations — bodies are **form-encoded**
  (`application/x-www-form-urlencoded`), not JSON.
- `/api/1` list operations page with `offset` + `count` and return
  `{offset, count, totalCount, result}`.
- Errors use the `{errorCode, message}` envelope. There is no idempotency key, but the
  consent writes above are state-setting rather than incrementing, so re-sending the
  same intended state is safe. Re-sending a *different* state is not.

## Related event surface

Act-On emits webhooks for every consent transition —
`contact-opt.global-opt-in`, `contact-opt.global-opt-out`,
`subscription-category.opt-in`, `subscription-category.opt-out`,
`contact-bounce.hard`, `contact-bounce.soft`,
`contact-email.marked-as-spam`. They are **configured in the Act-On UI**, not through
this API, so an integration cannot subscribe itself. See
`asyncapi/act-on-webhooks.yml`.
