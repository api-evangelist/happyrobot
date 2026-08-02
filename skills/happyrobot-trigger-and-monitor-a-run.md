---
name: Trigger a workflow run and monitor it to completion
description: Start a Happyrobot workflow run with a payload, then follow its sessions and messages to completion, pull recordings, and cancel or annotate it.
api: openapi/happyrobot-public-api-openapi.json
base_url: https://platform.happyrobot.ai/api/v2
operations:
  - POST /workflows/{workflow_id}/runs
  - GET /runs/{run_id}
  - GET /runs/{run_id}/sessions
  - GET /sessions/{session_id}/messages
  - GET /sessions/{session_id}/stream
  - GET /runs/{run_id}/recordings
  - POST /runs/{run_id}/cancel
  - POST /runs/{run_id}/mark
---

# Trigger a workflow run and monitor it

## Before you start

- Send `Authorization: Bearer <api_key>` on every request. The key is bound to one organization **and one
  environment** — there is no environment parameter on these operations. Confirm which one you hold with
  `GET /api-key/describe` (it returns `org_slug`, `prefix`, `lastFour` and `revokedAt`).
- **There is no idempotency key in this API.** If `POST /workflows/{workflow_id}/runs` times out, do not
  blindly retry — you will start a second run, and for a voice workflow that means a second phone call.
  Instead, list recent runs with `GET /workflows/{workflow_id}/runs` and match on your own correlation
  value before retrying.

## Steps

1. **Start the run.** `POST /workflows/{workflow_id}/runs` with your trigger payload.
   `workflow_id` accepts either the workflow UUID or its slug. Keep the returned `run_id`.
2. **Poll the run.** `GET /runs/{run_id}` for status. For a list view across a workflow use
   `GET /workflows/{workflow_id}/runs` — it paginates with `page` and `page_size` (not `cursor`).
3. **Find the conversation.** `GET /runs/{run_id}/sessions` returns the sessions the run produced; a voice
   run typically has one, a multi-channel run more.
4. **Read the transcript.** `GET /sessions/{session_id}/messages` for the completed record.
5. **Or stream it live.** `GET /sessions/{session_id}/stream` opens Server-Sent Events. It emits `message`
   events and closes when the session ends. Pass `backfillLimit` (0–1000, default 0) to replay recent
   messages on connect. Prefer this over polling — polling `/messages` in a loop is the wrong shape.
6. **Inspect node-level detail** when a run misbehaves: `GET /runs/{run_id}/nodes`, then
   `GET /runs/{run_id}/outputs/{output_id}` for a specific node output.
7. **Fetch audio.** `GET /runs/{run_id}/recordings`.
8. **Annotate.** `POST /runs/{run_id}/mark` to flag the run for review; `GET /runs/{run_id}/flags` to read
   existing flags. `GET /runs/{run_id}/audits` returns grading against the workflow's northstars.
9. **Stop it.** `POST /runs/{run_id}/cancel` — expect `403` if the run belongs to another organization and
   `404` if the id is unknown.

## Errors

Every error is `{ error, message, statusCode, details }` — **not** RFC 9457 problem+json, so do not look
for a `type` URI. Branch on the HTTP status:

- `401` — bad, missing or revoked key. Re-check with `GET /api-key/describe`.
- `403` — the key's organization does not own this run.
- `404` — unknown `run_id`, or a run in a different environment than the key.
- `502` — an upstream dependency (carrier, integration, workflow runtime) failed. Safe to retry a read;
  for `POST /runs/{run_id}/cancel`, re-read the run first to see whether the cancel actually landed.
- `500` — retry reads with backoff.

There is no `Retry-After` and no `RateLimit-*` header anywhere in this API, so use your own exponential
backoff. `429` is not declared on any run operation, only on phone-number and SIP-trunk provisioning.
