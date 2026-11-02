---
name: whatsapp-wasender-ops
description: >-
  Use this when sending WhatsApp messages or media through the Wasender REST
  API, including checks before sending and delivery confirmation.
---
# WhatsApp via Wasender

Use the Wasender REST API as the only WhatsApp channel.

## Before every send
1. Run the commands on the computer that is allowed to reach Wasender (the cloud box may be blocked by Cloudflare). Keep the API key in a secret store, never print it, and delete any temporary key or body file after use.
2. GET `/api/status` must say connected.
3. GET `/api/user` must return the expected sender number.
4. Verify the recipient number matches the intended person.

## Sending
- POST `/api/send-message` with Bearer key and body `{"to":"+E164","text":"..."}`.
- Put Hebrew or other non-ASCII text only inside a UTF-8 JSON body file, not inline in the command.
- Media is sent by public URL. Videos above 50MB must be compressed first (target about 38MB) and uploaded to a public host.
- If you get HTTP 429, wait about 12 seconds and retry once, only if no message was created.
- Send each message exactly once.

## Confirm
GET `/api/messages/{id}/info` and wait for status 3 (delivered). Do not report done on API success alone. Status 2 means sent to the server only; report it honestly. A message to the sender's own number may never show delivered.

## Rules
- Max two unanswered contact attempts to the same person on the same topic, then stop until the owner asks again.
- Do not contact anyone the owner has not approved.
