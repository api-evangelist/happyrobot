# Happyrobot

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

HappyRobot is an AI orchestration platform — "the AI operating system for the real economy" — that lets enterprises build, govern and deploy AI agents ("AI workers") into operational workflows across logistics, freight brokerage, 3PL, utilities, airlines, finance, insurance, manufacturing, retail and telecom. Agents place and answer phone calls, send and receive email, SMS, WhatsApp and chat, read and write to TMS/ERP systems, and execute multi-step workflows built as node graphs in a visual builder. The Happyrobot Public API (v2) exposes 205 operations across 32 resource families — workflows, versions and nodes, runs, sessions and messages, contacts and memories, knowledge bases, phone numbers and SIP trunks, integrations, chat and voice tokens, signals, billing, plus a full agent-governance surface (audits, northstars, custom evals, adversarial tests and suites). Authentication is a bearer API key scoped to an organization and an environment; the platform additionally runs an Auth0 OIDC tenant for human sign-in and an OAuth 2.0 authorization server for its MCP surface.

**Areas:** AI Agents · Agent Orchestration · Voice AI · Conversational AI · Logistics · Freight · Supply Chain · Workflow Automation · Contact Center · Telephony · MCP · Agent-Native

## Happyrobot on APIs.io

Everything profiled for Happyrobot is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/happyrobot/](https://apis.io/providers/happyrobot/)** — or go straight to one of the APIs or properties below.

### APIs (35)

- [Happyrobot Workflows MCP Server](https://apis.io/apis/happyrobot/happyrobot-workflows-mcp-server/) — Happyrobot's first-party remote MCP server for building and governing workflows — 26 published tools plus 5 MCP prompts, served over Streamable HTTP and…
- [Happyrobot Twin MCP Server](https://apis.io/apis/happyrobot/happyrobot-twin-mcp-server/) — First-party remote MCP server over the customer's Twin database — 9 published tools covering schema introspection, paginated reads, table creation, row…
- [Happyrobot Docs MCP Server](https://apis.io/apis/happyrobot/happyrobot-docs-mcp-server/) — A hosted documentation-search MCP server on the docs host, discovered via RFC 9728 protected-resource metadata at…
- [Happyrobot Adversarial Suites API](https://apis.io/apis/happyrobot/happyrobot-adversarial-suites-api/) — The Adversarial Suites API from Happyrobot — 8 operation(s) for adversarial suites.
- [Happyrobot Adversarial Tests API](https://apis.io/apis/happyrobot/happyrobot-adversarial-tests-api/) — The Adversarial Tests API from Happyrobot — 8 operation(s) for adversarial tests.
- [Happyrobot API Keys API](https://apis.io/apis/happyrobot/happyrobot-api-keys-api/) — The API Keys API from Happyrobot — 1 operation(s) for api keys.
- [Happyrobot Apps API](https://apis.io/apis/happyrobot/happyrobot-apps-api/) — The Apps API from Happyrobot — 1 operation(s) for apps.
- [Happyrobot Artifacts API](https://apis.io/apis/happyrobot/happyrobot-artifacts-api/) — The Artifacts API from Happyrobot — 1 operation(s) for artifacts.
- [Happyrobot Audits API](https://apis.io/apis/happyrobot/happyrobot-audits-api/) — The Audits API from Happyrobot — 8 operation(s) for audits.
- [Happyrobot Billing API](https://apis.io/apis/happyrobot/happyrobot-billing-api/) — The Billing API from Happyrobot — 4 operation(s) for billing.
- [Happyrobot Chat API](https://apis.io/apis/happyrobot/happyrobot-chat-api/) — The Chat API from Happyrobot — 7 operation(s) for chat.
- [Happyrobot Contacts API](https://apis.io/apis/happyrobot/happyrobot-contacts-api/) — The Contacts API from Happyrobot — 5 operation(s) for contacts.
- [Happyrobot Custom Evals API](https://apis.io/apis/happyrobot/happyrobot-custom-evals-api/) — The Custom Evals API from Happyrobot — 8 operation(s) for custom evals.
- [Happyrobot Events API](https://apis.io/apis/happyrobot/happyrobot-events-api/) — The Events API from Happyrobot — 1 operation(s) for events.
- [Happyrobot Integration Resources API](https://apis.io/apis/happyrobot/happyrobot-integration-resources-api/) — The Integration Resources API from Happyrobot — 15 operation(s) for integration resources.
- [Happyrobot Integrations API](https://apis.io/apis/happyrobot/happyrobot-integrations-api/) — The Integrations API from Happyrobot — 4 operation(s) for integrations.
- [Happyrobot Issues API](https://apis.io/apis/happyrobot/happyrobot-issues-api/) — The Issues API from Happyrobot — 3 operation(s) for issues.
- [Happyrobot Knowledge Bases API](https://apis.io/apis/happyrobot/happyrobot-knowledge-bases-api/) — The Knowledge Bases API from Happyrobot — 6 operation(s) for knowledge bases.
- [Happyrobot MCP Servers API](https://apis.io/apis/happyrobot/happyrobot-mcp-servers-api/) — The MCP Servers API from Happyrobot — 3 operation(s) for mcp servers.
- [Happyrobot Messages API](https://apis.io/apis/happyrobot/happyrobot-messages-api/) — The Messages API from Happyrobot — 1 operation(s) for messages.
- [Happyrobot Northstars API](https://apis.io/apis/happyrobot/happyrobot-northstars-api/) — The Northstars API from Happyrobot — 9 operation(s) for northstars.
- [Happyrobot Organization API](https://apis.io/apis/happyrobot/happyrobot-organization-api/) — The Organization API from Happyrobot — 2 operation(s) for organization.
- [Happyrobot Phone Numbers API](https://apis.io/apis/happyrobot/happyrobot-phone-numbers-api/) — The Phone Numbers API from Happyrobot — 10 operation(s) for phone numbers.
- [Happyrobot Realtime API](https://apis.io/apis/happyrobot/happyrobot-realtime-api/) — The Realtime API from Happyrobot — 1 operation(s) for realtime.
- [Happyrobot Runs API](https://apis.io/apis/happyrobot/happyrobot-runs-api/) — The Runs API from Happyrobot — 12 operation(s) for runs.
- [Happyrobot Sessions API](https://apis.io/apis/happyrobot/happyrobot-sessions-api/) — The Sessions API from Happyrobot — 4 operation(s) for sessions.
- [Happyrobot Signals API](https://apis.io/apis/happyrobot/happyrobot-signals-api/) — The Signals API from Happyrobot — 4 operation(s) for signals.
- [Happyrobot SIP Trunks API](https://apis.io/apis/happyrobot/happyrobot-sip-trunks-api/) — The SIP Trunks API from Happyrobot — 4 operation(s) for sip trunks.
- [Happyrobot Twin API](https://apis.io/apis/happyrobot/happyrobot-twin-api/) — The Twin API from Happyrobot — 6 operation(s) for twin.
- [Happyrobot Use Cases API](https://apis.io/apis/happyrobot/happyrobot-use-cases-api/) — The Use Cases API from Happyrobot — 1 operation(s) for use cases.
- [Happyrobot Versions API](https://apis.io/apis/happyrobot/happyrobot-versions-api/) — The Versions API from Happyrobot — 16 operation(s) for versions.
- [Happyrobot Voice API](https://apis.io/apis/happyrobot/happyrobot-voice-api/) — The Voice API from Happyrobot — 1 operation(s) for voice.
- [Happyrobot Workflow Folders API](https://apis.io/apis/happyrobot/happyrobot-workflow-folders-api/) — The Workflow Folders API from Happyrobot — 2 operation(s) for workflow folders.
- [Happyrobot Workflow Variables API](https://apis.io/apis/happyrobot/happyrobot-workflow-variables-api/) — The Workflow Variables API from Happyrobot — 2 operation(s) for workflow variables.
- [Happyrobot Workflows API](https://apis.io/apis/happyrobot/happyrobot-workflows-api/) — The Workflows API from Happyrobot — 10 operation(s) for workflows.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Happyrobot Events](https://apis.io/asyncapis/happyrobot/happyrobot-events/)

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [happyrobot-mcp.yml](https://apis.io/servers/happyrobot/happyrobot-mcp-yml/)
- [mcp](https://apis.io/servers/happyrobot/mcp/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Happyrobot Agentic Access](https://apis.io/agentic-access/happyrobot/happyrobot-agentic-access/)

#### Collections (2)

Postman and Open Collection request collections.

- [Happyrobot Platform API](https://apis.io/collections/happyrobot/open-happyrobot-platform-v1/)
- [Happyrobot Public API](https://apis.io/collections/happyrobot/open-happyrobot-public-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Happyrobot Public Api Overlay](https://apis.io/overlays/happyrobot/happyrobot-public-api-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Happyrobot Authentication](https://apis.io/security/happyrobot/happyrobot-authentication/)
- [Happyrobot Domain Security](https://apis.io/security/happyrobot/happyrobot-domain-security/)
- [Happyrobot Trust Center](https://apis.io/security/happyrobot/happyrobot-trust-center/)
- [Happyrobot Vulnerability Disclosure](https://apis.io/security/happyrobot/happyrobot-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Happyrobot Scopes](https://apis.io/scopes/happyrobot/happyrobot-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.happyrobot.ai/)
- [Documentation](https://docs.happyrobot.ai)
- [Getting started](https://docs.happyrobot.ai/getting_started)
- [API reference](https://docs.happyrobot.ai/api-reference)
- [Pricing](https://docs.happyrobot.ai/general/pricing)
- [Sign up](https://app.happyrobot.ai/signup)
- [Support](https://www.happyrobot.ai/contact)
- [Blog](https://www.happyrobot.ai/blog)
- [Security](https://happyrobot.ai/.well-known/security.txt)
- [Compliance](https://www.happyrobot.ai/product/security-and-reliability)
- [Trust centre](https://trust.happyrobot.ai/)
- [Terms of service](https://www.happyrobot.ai/legal/terms-and-conditions)
- [Privacy policy](https://www.happyrobot.ai/legal/privacy-policy)
- [GitHub](https://github.com/happyrobot-ai)
- [Status](https://status.happyrobot.ai/)

## API Evangelist rating

**Kin Score 46.2** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 55.4 |
| Contract governance | 18.2 |
| Operational transparency | 31.6 |
| Developer ergonomics | 35.1 |
| Access clarity | 35.5 |

**Agent readiness 48.4** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 45.1** — AI & Biometrics

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/happyrobot/](https://apis.io/providers/happyrobot/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Happyrobot: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/happyrobot/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
