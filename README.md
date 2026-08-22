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

HappyRobot is an AI orchestration platform — "the AI operating system for the real economy" — that lets
enterprises build, govern and deploy AI agents into operational workflows across logistics, freight
brokerage, 3PL, utilities, airlines, finance, insurance, manufacturing, retail and telecom. Agents place
and answer calls, send and receive email, SMS, WhatsApp and chat, read and write to TMS/ERP systems, and
run multi-step workflows built as node graphs.

- Website: https://www.happyrobot.ai/
- Docs: https://docs.happyrobot.ai (access-gated)
- Status: https://status.happyrobot.ai/
- Trust center: https://trust.happyrobot.ai/
- GitHub: https://github.com/happyrobot-ai

## APIs

| API | Base URL | Spec |
|---|---|---|
| Happyrobot Public API (v2) | `https://platform.happyrobot.ai/api/v2` | OpenAPI 3.0.3 — 162 paths, 205 operations |
| Happyrobot Public API (EU) | `https://platform.eu.happyrobot.ai/api/v2` | same document, EU data-residency cluster |
| Happyrobot Platform API (v1, legacy) | `https://platform.happyrobot.ai/api/v1` | OpenAPI 3.0.2 — 10 read-only operations |
| Workflows MCP Server | `https://mcp.platform.happyrobot.ai/workflows/mcp` | 26 tools + 5 prompts, OAuth `mcp:full` |
| Twin MCP Server | `https://mcp.platform.happyrobot.ai/twin/mcp` | 9 tools, OAuth `mcp:full` |
| Docs MCP Server | `https://docs.happyrobot.ai/mcp` | documentation search, OAuth `mcp:search` |

The v2 OpenAPI is served publicly and anonymously from the API host at `/api/v2/docs/json` — not from the
docs host, which returns an application shell for every path.

## Artifacts

`openapi/` · `authentication/` · `scopes/` · `conventions/` · `errors/` · `asyncapi/` · `data-model/` ·
`mcp/` · `lifecycle/` · `conformance/` · `sandbox/` · `components/` · `packages/` · `security/` ·
`well-known/` · `overlays/` · `agentic-access/` · `skills/` · `llms/`

## Notable findings

- **Four first-party MCP servers**, two of them full remote Streamable HTTP endpoints with RFC 9728
  protected-resource metadata and RFC 7591 dynamic client registration. The MCP surface is
  *builder*-shaped: all 26 Workflows tools author, version, test and govern workflows, and bind to 150 of
  the 205 REST operations. The runtime data plane — contacts, memories, sessions, messages, knowledge
  bases, billing — is REST-only (55 operations with no tool).
- **A deep agent-governance surface in the API itself**: northstars (declarative success criteria),
  custom evals extractable from real production runs, adversarial red-team tests and batched suites, and
  post-hoc audits. Rare among agent platforms.
- **No idempotency contract anywhere** — the string "idempot" does not appear in either spec, including on
  operations that purchase phone numbers or start voice calls.
- **Errors are not RFC 9457**, and use three different envelope shapes.
- **No A2A agent card** on any host.
- **The documentation is access-gated** while the OpenAPI is wide open — an unusual inversion.

Profiled by the API Evangelist enrichment pipeline, 2026-08-01.
