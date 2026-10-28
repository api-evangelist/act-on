# Act-On

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Act-On Software is a cloud-based marketing automation platform used by B2B and B2C marketing teams for email marketing, lead generation and nurturing, landing pages and forms, website visitor tracking, lead scoring and segmentation, custom data, and campaign reporting. Act-On publishes four OpenAPI 3.1 documents through its developer portal covering 158 operations on one gateway host (https://api.actonsoftware.com, with an EU region at api-eu.actonsoftware.com): the legacy form-encoded /api/1 surface, the newer JSON Act-On Contacts layer at /ucl/v2, a transactional email endpoint at /ete/v1, and a separately versioned Custom Objects Service at /custom-objects/v1 that is in request-only beta. Authentication is OAuth 2.0 with password, refresh_token and authorization_code grants and no scopes. Act-On also ships a signed outgoing-webhook event surface with nineteen documented event types. Added to the API Evangelist network from a Norwest Venture Partners portfolio lead and enriched from Act-On's public developer surface.

**Areas:** Company · Marketing · Marketing Automation · Email Marketing · Email · Marketing Technology · Lead Generation · Campaign Management · Customer Data · Webhook

## Act-On on APIs.io

Everything profiled for Act-On is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/act-on/](https://apis.io/providers/act-on/)** — or go straight to one of the APIs or properties below.

### APIs (25)

- [Act-On Outgoing Webhooks](https://apis.io/apis/act-on/act-on-outgoing-webhooks/) — Outgoing webhook event surface — nineteen documented event types across contacts, consent, deliverability, lead scoring, subscriptions, automated programs,…
- [Act-On Account API](https://apis.io/apis/act-on/act-on-account-api/) — The Account API from Act-On — 1 operation(s) for account.
- [Act-On Campaigns API](https://apis.io/apis/act-on/act-on-campaigns-api/) — The Campaigns API from Act-On — 2 operation(s) for campaigns.
- [Act-On Custom Data Dataset API](https://apis.io/apis/act-on/act-on-custom-data-dataset-api-api/) — Custom Data Dataset API
- [Act-On Custom Data Query API](https://apis.io/apis/act-on/act-on-custom-data-query-api-api/) — Custom Data Query API
- [Act-On Custom Data Schema API](https://apis.io/apis/act-on/act-on-custom-data-schema-api-api/) — Custom Data Schema API
- [Act-On Ete API](https://apis.io/apis/act-on/act-on-ete-api/) — The Ete API from Act-On — 1 operation(s) for ete.
- [Act-On Footer API](https://apis.io/apis/act-on/act-on-footer-api/) — The Footer API from Act-On — 3 operation(s) for footer.
- [Act-On Form API](https://apis.io/apis/act-on/act-on-form-api/) — The Form API from Act-On — 3 operation(s) for form.
- [Act-On Header API](https://apis.io/apis/act-on/act-on-header-api/) — The Header API from Act-On — 3 operation(s) for header.
- [Act-On Image API](https://apis.io/apis/act-on/act-on-image-api/) — The Image API from Act-On — 2 operation(s) for image.
- [Act-On List API](https://apis.io/apis/act-on/act-on-list-api/) — The List API from Act-On — 13 operation(s) for list.
- [Act-On Logo API](https://apis.io/apis/act-on/act-on-logo-api/) — The Logo API from Act-On — 2 operation(s) for logo.
- [Act-On Media API](https://apis.io/apis/act-on/act-on-media-api/) — The Media API from Act-On — 7 operation(s) for media.
- [Act-On Medialink API](https://apis.io/apis/act-on/act-on-medialink-api/) — The Medialink API from Act-On — 1 operation(s) for medialink.
- [Act-On Message API](https://apis.io/apis/act-on/act-on-message-api/) — The Message API from Act-On — 8 operation(s) for message.
- [Act-On Page API](https://apis.io/apis/act-on/act-on-page-api/) — The Page API from Act-On — 4 operation(s) for page.
- [Act-On Program API](https://apis.io/apis/act-on/act-on-program-api/) — The Program API from Act-On — 1 operation(s) for program.
- [Act-On Seokeywords API](https://apis.io/apis/act-on/act-on-seokeywords-api/) — The Seokeywords API from Act-On — 1 operation(s) for seokeywords.
- [Act-On Seoreport API](https://apis.io/apis/act-on/act-on-seoreport-api/) — The Seoreport API from Act-On — 1 operation(s) for seoreport.
- [Act-On Subscription API](https://apis.io/apis/act-on/act-on-subscription-api/) — The Subscription API from Act-On — 3 operation(s) for subscription.
- [Act-On Token API](https://apis.io/apis/act-on/act-on-token-api/) — The Token API from Act-On — 1 operation(s) for token.
- [Act-On Ucl API](https://apis.io/apis/act-on/act-on-ucl-api/) — The Ucl API from Act-On — 30 operation(s) for ucl.
- [Act-On User API](https://apis.io/apis/act-on/act-on-user-api/) — The User API from Act-On — 3 operation(s) for user.
- [Act-On Custom Events API](https://apis.io/apis/act-on/act-on-custom-events-api/) — The Custom Events API from Act-On — 2 operation(s) for custom events.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Act On Webhooks](https://apis.io/asyncapis/act-on/act-on-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [act-on-mcp.yml](https://apis.io/servers/act-on/act-on-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Act On Agentic Access](https://apis.io/agentic-access/act-on/act-on-agentic-access/)

#### JSON Schema (7)

The data models the API reads and writes.

- [CreateDatasetRequestDTO](https://apis.io/schemas/act-on/act-on-create-dataset-request-dto/)
- [CreateSchemaRequestDTO](https://apis.io/schemas/act-on/act-on-create-schema-request-dto/)
- [DataQueryRequestDTO](https://apis.io/schemas/act-on/act-on-data-query-request-dto/)
- [DeleteRecordsRequestDTO](https://apis.io/schemas/act-on/act-on-delete-records-request-dto/)
- [FieldDefinitionDTO](https://apis.io/schemas/act-on/act-on-field-definition-dto/)
- [UpdateDatasetRequestDTO](https://apis.io/schemas/act-on/act-on-update-dataset-request-dto/)
- [ValidationRequestDTO](https://apis.io/schemas/act-on/act-on-validation-request-dto/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Act On Context](https://apis.io/jsonld/act-on/act-on-context/)

#### Collections (4)

Postman and Open Collection request collections.

- [Custom Objects Service](https://apis.io/collections/act-on/open-act-on-custom-objects-service/)
- [oauth](https://apis.io/collections/act-on/open-act-on-oauth/)
- [act-on-api-raw-body](https://apis.io/collections/act-on/open-act-on-raw-body-api/)
- [act-on-api-1](https://apis.io/collections/act-on/open-act-on-rest-api/)

#### Overlays (4)

OpenAPI overlays, including conversational phrasing for each operation.

- [Act On Custom Objects Service Overlay](https://apis.io/overlays/act-on/act-on-custom-objects-service-overlay/)
- [Act On Oauth Overlay](https://apis.io/overlays/act-on/act-on-oauth-overlay/)
- [Act On Raw Body Api Overlay](https://apis.io/overlays/act-on/act-on-raw-body-api-overlay/)
- [Act On Rest Api Overlay](https://apis.io/overlays/act-on/act-on-rest-api-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Act-On API Rules](https://apis.io/rules/act-on/act-on-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Act On Authentication](https://apis.io/security/act-on/act-on-authentication/)
- [Act On Domain Security](https://apis.io/security/act-on/act-on-domain-security/)
- [Act On Trust Center](https://apis.io/security/act-on/act-on-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Act On Scopes](https://apis.io/scopes/act-on/act-on-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Act On Plans Pricing](https://apis.io/plans/act-on/act-on-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Act On Rate Limits](https://apis.io/rate-limits/act-on/act-on-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://act-on.com)
- [Documentation](https://developer.act-on.com)
- [Getting started](https://developer.act-on.com/reference/request-a-developer-account)
- [API reference](https://developer.act-on.com/reference/api-overview)
- [Pricing](https://act-on.com/pricing/)
- [Support](https://act-on.com/product/services/support-packages/)
- [Changelog](https://connect.act-on.com/hc/en-us/categories/13386837131927-What-s-New)
- [Blog](https://act-on.com/learn/blog/)
- [Terms of service](https://act-on.com/terms-of-service/)
- [Privacy policy](https://act-on.com/privacy-policy/)
- [Status](https://status.act-on.com)

## API Evangelist rating

**Kin Score 66.1** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 73.0 |
| Contract governance | 22.0 |
| Operational transparency | 89.5 |
| Developer ergonomics | 55.4 |
| Access clarity | 36.8 |

**Agent readiness 49.8** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | yes |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 31.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/act-on/](https://apis.io/providers/act-on/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Act-On: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/act-on/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
