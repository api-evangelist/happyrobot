# Happyrobot

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
