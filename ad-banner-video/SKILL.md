---
name: מודעות
description: >-
  Use when the owner asks for an ad/marketing banner video (סקיל מודעות): APIhub
  banner/motion-gold, 15s square 1080x1080, via POST /v1/banner with
  estimate-first.
---
# מודעות: APIhub banner/motion-gold

Recipe source (fetch fresh each time): https://apihub.co.il/skills/banner-motion-gold.md
Docs: https://apihub.co.il/docs · skills index: https://apihub.co.il/skills/index.md

## Steps
1. Need brief (what, price, gift, place, audience), business name, optional logo URL and own media. If missing, ask one short question. Never invent price/discount/gift/number/place.
2. Fetch the recipe and follow it in order.
3. Body:
```json
{"brief":"<offer in customer words>","style":"motion-gold","language":"he","business":{"name":"<name>"},"media":"own"}
```
Add business.logo_url when a public logo link is given.
4. POST same body to /v1/banner/estimate → estimated_credits. Tell the user the price and WAIT for OK.
5. POST /v1/banner with headers Authorization: Bearer $APIHUB_API_KEY, Content-Type: application/json, X-Tag: <job tag>, Idempotency-Key: <tag>-make, x-wait-ms: 90000. Poll GET /v1/executions/{id} every 5s while processing. Retry with the SAME idempotency key if unsure.
6. Text edits later: POST output.plan to /v1/banner/render (only render is paid), never remake.
7. Download the video and poster right away (links expire in 24h). Save the video as MP4 (video/mp4) to the מוכן Drive folder. Do not publish.
8. Report: link + poster, caption + hashtags returned, cost via GET /v1/usage?tag=<tag> → totals.credits.

Errors: 400 fix named field · 401 bad key · 402 no credits (tell user) · 429 wait & retry. Never show the key.
