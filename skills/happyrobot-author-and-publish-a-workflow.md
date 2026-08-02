---
name: Author, test and publish a workflow version
description: Create a Happyrobot workflow, fork a version, add and configure nodes against their real config schemas, test every node, then lock and publish.
api: openapi/happyrobot-public-api-openapi.json
base_url: https://platform.happyrobot.ai/api/v2
operations:
  - GET /workflows/templates
  - POST /workflows/
  - GET /workflows/{workflow_id}/versions
  - POST /versions/{version_id}/fork
  - GET /events/{event_id}/config-schema
  - POST /versions/{version_id}/nodes
  - GET /versions/{version_id}/nodes/{node_id}/available-vars
  - POST /versions/{version_id}/test-all
  - POST /versions/{version_id}/lock
  - POST /versions/{version_id}/publish
---

# Author, test and publish a workflow version

Happyrobot versions the *workflow itself* as a first-class resource. Never edit a published version —
fork it, edit the fork, test, lock, publish.

## Steps

1. **Start from a template or from scratch.** `GET /workflows/templates` lists templates;
   `POST /workflows/` creates the workflow. Use `GET /workflow-folders/` and `POST /workflow-folders/` to
   place it in the folder tree (folders nest via `parent_folder_id`).
2. **Get a working version.** `GET /workflows/{workflow_id}/versions`, then
   `POST /versions/{version_id}/fork` to branch off the published one. Work only on the fork.
3. **Learn what a node needs before you build it.** Every node is configured from an event. Call
   `GET /events/{event_id}/config-schema` first — it returns field types, required fields, defaults and
   available options. Do not guess a node's configuration shape; ask for its schema.
4. **Add nodes.** `POST /versions/{version_id}/nodes`. Non-trigger nodes need a parent — either
   `parent_node_id` or `parent_index` (index of the parent within the same request's `nodes` array).
   These two are mutually exclusive.
   - For a **webhook trigger** (`INCOMING_HOOK` or `PREDEFINED_REQUEST`), set `webhook_payload` to the
     payload you expect. It is saved as the node's output so downstream nodes can reference it — this is
     how you get variables to bind against before any real traffic arrives.
5. **Wire variables correctly.** `GET /versions/{version_id}/nodes/{node_id}/available-vars` returns the
   upstream variables actually reachable from a node. Use it rather than inferring names. Reference by
   index (`{{index.field}}`) or by the stable `persistent_id` (`{{persistent_id.field}}`) — `persistent_id`
   survives a fork, `node_id` does not.
6. **Edit a node.** `PUT /versions/{version_id}/nodes/{node_id}`. The body must carry a `type`
   discriminator matching the node type; updatable fields differ by type (trigger/action take `name`,
   `configuration`, `webhook_payload`; agent takes `prompt`; tool takes `function`).
   `PUT /versions/{version_id}/nodes/{node_id}/custom-output` pins an output without running the node.
7. **Check your work.** `GET /versions/{version_id}/prompt-issues` surfaces prompt-quality problems;
   `GET /workflows/{workflow_id}/issues` lists workflow-level ones; `PATCH /issues/{issue_id}` resolves.
8. **Test everything.** `POST /versions/{version_id}/test-all` with
   `{"environment": "development" | "staging" | "production"}` (default `development`). It runs every
   testable node in dependency waves, parallelising independent nodes, skipping dependents of a failure,
   and blocks until done. **This is the only operation in the API that declares a 504** — set a generous
   client timeout. For one node, use `POST /versions/{version_id}/nodes/{node_id}/test`.
9. **Freeze and ship.** `POST /versions/{version_id}/lock`, then `POST /versions/{version_id}/publish`.
   Inverses are `POST /versions/{version_id}/unlock` and `.../unpublish`.
10. **Get the live webhook URLs.** After publishing, `GET /versions/{version_id}/nodes/{node_id}` on a
    webhook trigger node returns `webhook_urls` with a separate URL for `production`, `staging`,
    `development` and `test` (the test URL targets that specific version).

## Rules

- Variables are per workflow **and** per environment: `GET/POST /workflows/{workflow_id}/variables` and
  `PATCH|DELETE /workflows/{workflow_id}/variables/{variable_id}`. A value set in development does not
  exist in production.
- Node collections paginate with `page` and `page_size`.
- No idempotency key exists. `POST /versions/{version_id}/nodes` retried after a timeout can duplicate a
  node — re-read `GET /versions/{version_id}/nodes` before retrying.
- `409` on the knowledge-base family returns `{ message }` only, with no `error` field. Handle both
  envelope shapes.
