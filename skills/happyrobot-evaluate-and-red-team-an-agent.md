---
name: Evaluate and red-team an agent node before shipping it
description: Use Happyrobot's northstars, custom evals, adversarial tests and audits to prove an agent node behaves before publishing it to production.
api: openapi/happyrobot-public-api-openapi.json
base_url: https://platform.happyrobot.ai/api/v2
operations:
  - GET /nodes/{node_id}/northstars
  - POST /nodes/{node_id}/northstars/generate
  - POST /nodes/{node_id}/northstars/assess-coverage
  - POST /nodes/{node_id}/custom-evals/extract-from-run
  - POST /custom-evals/{eval_id}/run
  - POST /nodes/{node_id}/adversarial-tests
  - POST /adversarial-suites/{suite_id}/generate
  - POST /adversarial-suites/{suite_id}/run
  - GET /adversarial-suites/runs/{suite_run_id}/test-runs
  - GET /workflows/{workflow_id}/audits/stats
---

# Evaluate and red-team an agent node

Happyrobot's quality layer attaches to a **node**, not to a workflow — which is why almost every path
here starts `/nodes/{node_id}/`. Four mechanisms stack, from softest to hardest.

## 1. Northstars — declarative success criteria (prompt nodes)

- `GET /nodes/{node_id}/northstars` / `POST /nodes/{node_id}/northstars` to list and create.
- `POST /nodes/{node_id}/northstars/generate` drafts them for you from the node's prompt.
- `POST /nodes/{node_id}/northstars/iterate` refines an existing set.
- `POST /nodes/{node_id}/northstars/assess-coverage` tells you where the criteria are thin — run this
  before you trust a passing score.
- `PATCH /nodes/{node_id}/northstars/batch-toggle` to enable or disable in bulk.
- `GET /northstars/{northstar_id}/history` shows how a criterion evolved; regenerated criteria link back
  through `regenerated_from_northstar_id`.
- Organise with `POST /nodes/{node_id}/northstars/folders`.

## 2. Custom evals — concrete assertions (prompt nodes)

- `GET /nodes/{node_id}/custom-evals/default-variables` and `.../tools` tell you what an eval can assert
  against.
- **Turn a real incident into a regression test:**
  `POST /nodes/{node_id}/custom-evals/extract-from-run` builds an eval from an actual production run.
  This is the highest-value operation in this skill — prefer it over writing evals from imagination.
- `POST /custom-evals/{eval_id}/run`, then `GET /custom-evals/{eval_id}/runs` for results.
- `GET|PATCH|DELETE /custom-evals/{eval_id}` to manage.

## 3. Adversarial tests — red-teaming (agent nodes)

- `POST /nodes/{node_id}/adversarial-tests` creates one; `GET` lists them.
- `GET /adversarial-tests/{test_id}/effective-scope` shows what the test is actually allowed to probe —
  check this before believing a pass.
- `POST /adversarial-tests/{test_id}/run`, then `GET /adversarial-tests/runs/{run_id}` and
  `GET /adversarial-tests/runs/{run_id}/messages` to read the full attack transcript.

## 4. Adversarial suites — batched red-teaming

- `GET|POST /nodes/{node_id}/adversarial-suites`.
- `POST /adversarial-suites/{suite_id}/generate` and `.../generate-graph` build the suite.
- `POST /adversarial-suites/{suite_id}/run` executes it.
- `GET /adversarial-suites/runs/{suite_run_id}` for the roll-up and
  `GET /adversarial-suites/runs/{suite_run_id}/test-runs` for the per-test detail.

## 5. Audits — grade what actually happened in production

- `GET /workflows/{workflow_id}/audits/stats` for the summary.
- `GET /workflows/{workflow_id}/audits/northstars` for per-criterion performance and
  `.../audits/northstars/{northstar_id}/remarks` for the individual remarks
  (**cursor-paginated with `cursor` + `limit`, not `page`/`page_size`** — filterable by `grade` and
  `status`).
- `GET /workflows/{workflow_id}/audits/node-errors` for failures by node.
- `GET /workflows/{workflow_id}/audits/versions` compares versions.
- `GET /runs/{run_id}/audits` grades one run.
- Feed back with `POST|GET|DELETE /audit-remarks/{audit_remark_id}/feedback`.

## Suggested order

`assess-coverage` → fix the northstars → `extract-from-run` for every known failure → run the custom evals
→ run an adversarial suite → only then `POST /versions/{version_id}/lock` and `.../publish`.

## Notes

- Suite and test runs are asynchronous — poll the `runs` collections; there is no webhook for completion
  in the published contract.
- These operations declare `500` and `502` broadly. Retry reads with your own backoff; there is no
  `Retry-After`.
