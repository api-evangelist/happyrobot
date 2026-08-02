---
name: Provision a phone number and attach it to a workflow
description: Buy or bring a phone number, wire a SIP trunk, run toll-free verification, attach the number to a workflow, and track usage.
api: openapi/happyrobot-public-api-openapi.json
base_url: https://platform.happyrobot.ai/api/v2
operations:
  - GET /phone-numbers/
  - POST /phone-numbers/
  - PUT /phone-numbers/{id}
  - POST /phone-numbers/sip-trunk
  - GET /sip-trunks/options
  - POST /sip-trunks/
  - POST /phone-numbers/validate-toll-free-numbers
  - POST /phone-numbers/tollfree-verification
  - POST /phone-numbers/remove-from-workflow
  - GET /phone-numbers/usage
---

# Provision a phone number and attach it to a workflow

**This skill spends money and touches real carrier inventory.** There are no magic test numbers in this
API, and no idempotency key. Treat every write here as non-repeatable.

## Steps

1. **See what you already have.** `GET /phone-numbers/` (paginates with `page` / `page_size`). Check here
   before buying anything — a duplicate purchase is not reversible by retrying.
2. **Purchase.** `POST /phone-numbers/`. This is one of only three operations in the whole API that
   declares `429`, so be prepared to back off — but note there is **no `Retry-After` header**, so use your
   own exponential backoff and re-list numbers before each retry to avoid double-buying.
3. **Or bring your own trunk.** `GET /sip-trunks/options` for the supported configuration, then
   `POST /sip-trunks/` (also `429`-capable) or `POST /sip-trunks/bulk` for many. Manage with
   `GET|PUT|DELETE /sip-trunks/{id}`. Attach a trunk to a number with `POST /phone-numbers/sip-trunk`.
   Trunks carry distinct inbound and outbound roles (`inbound_trunk_id`, `outbound_trunk_id`).
4. **Toll-free numbers need verification before they will carry traffic.**
   - `POST /phone-numbers/validate-toll-free-numbers` to check candidates.
   - `POST /phone-numbers/tollfree-verification` to submit.
   - `GET /phone-numbers/tollfree-verification` to poll status.
   - `DELETE /phone-numbers/tollfree-verification/{verification_sid}` to withdraw.
   The `verification_sid` is carrier-supplied, not a Happyrobot UUID.
5. **Attach to a workflow.** `PUT /phone-numbers/{id}` sets the number's assignment.
   `POST /phone-numbers/remove-from-workflow` detaches it without releasing it.
6. **Release.** `POST /phone-numbers/free-up-number` frees a number for reassignment;
   `POST /phone-numbers/delete-number` releases it entirely. Note these are POST operations, not DELETE.
7. **Track spend.** `GET /phone-numbers/usage`, and `GET /billing/usage/totals`,
   `GET /billing/usage/details`, `GET /billing/usage/credits` for the account picture.

## Errors

- `429` — only on `POST /phone-numbers/`, `POST /sip-trunks/` and `POST /sip-trunks/bulk`. No backoff hint
  is provided.
- `503` — `GET /billing/usage/credits` can be unavailable; retry.
- `403` — the number belongs to another organization.
- Envelope is `{ error, message, statusCode, details }`.
