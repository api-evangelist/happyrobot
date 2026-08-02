---
name: Embed a browser chat session without exposing the API key
description: Use Happyrobot's two-tier token model to run an agent chat in the browser — the server holds the API key, the browser holds only a short-lived scoped token.
api: openapi/happyrobot-public-api-openapi.json
base_url: https://platform.happyrobot.ai/api/v2
operations:
  - POST /chat/tokens/
  - POST /chat/sessions/
  - POST /chat/sessions/{id}/messages
  - GET /chat/sessions/{id}/history
  - GET /chat/upload/presigned
  - POST /chat/upload/complete
  - POST /chat/sessions/{id}/close
---

# Embed a browser chat session

## The rule that matters

**Never ship `sk_live_…` to a browser.** Happyrobot's chat surface is designed around a two-tier
exchange: your server uses the API key once to mint a short-lived, workflow-scoped client token, and the
browser uses only that token for the rest of the session.

## Steps

### On your server (holds the API key)

1. `POST /chat/tokens/` with `{ "workflow_id": "<id>" }` and `Authorization: Bearer <api_key>`.
   Returns `{ token, expires_at }`. Return only that to the browser — never the key.

### In the browser (holds only the token)

2. `POST /chat/sessions/` with the client token. Returns a `session_id`.
3. Send messages with `POST /chat/sessions/{id}/messages`, or connect the WebSocket
   `WS /chat/sessions/{id}/ws?token=<JWT>` for streaming. The socket frames are `connected`,
   `message` (client → server, with `content`), `message-ack`, and streamed events.
   The WebSocket is not described in the OpenAPI — it is documented in Happyrobot's own
   `chatbot-sdk-example` repository.
4. Replay history with `GET /chat/sessions/{id}/history`.
5. **Attachments go out of band.** `GET /chat/upload/presigned` for an upload URL, PUT the bytes to that
   URL directly, then `POST /chat/upload/complete`. Do not try to multipart-POST files at the API —
   every declared request body in this API is `application/json`.
6. `POST /chat/sessions/{id}/close` when the user leaves.

### Voice is the same shape

`POST /voice/tokens/` returns `{ url, token, room_name, run_id }`; the browser connects over WebRTC to
LiveKit with that token. `POST /realtime/tokens` covers the realtime variant.

## Client libraries

Rather than hand-rolling this, use the first-party SDK — `@happyrobot-ai/sdk` for the server
(`client.chat.createToken`, `client.voice.createToken`) and `@happyrobot-ai/sdk/chat` /
`@happyrobot-ai/sdk/voice` in the browser (`HappyRobotChatClient`, `HappyRobotVoiceClient`).

## Errors

- `401` on the token exchange — bad API key.
- `401` in the browser — the client token expired; mint a new one server-side. Honour `expires_at`.
- `413` on `POST /chat/upload/complete` — payload too large. This response uses a **different envelope**:
  `{ error, statusCode }` with no `message` and no `details`.
- `503` on the upload operations — retry.
