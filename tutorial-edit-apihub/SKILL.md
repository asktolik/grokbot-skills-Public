---
name: הדרכה
description: >-
  Use this for the owner's regular tutorial/הדרכה videos (Loom, Zoom recordings,
  screen recordings; name: הדרכה): one APIhub render with marker + active-word
  box + extruded text + typewriter cursor, dead-segment trimming, slightly
  faster pace and pleasant light background music. Default for any video the owner
  calls הדרכה. For the vertical split-screen style use the skill named הדרכה מסך
  מפוצל.
---
# הדרכה (Tutorial) edit via APIhub — (skill name = "הדרכה"; the split-screen variant is "הדרכה מסך מפוצל")

Recipe (read first, public GET, no key): https://apihub.co.il/skills/effect-marker-sweep+effect-active-word-box+effect-extruded-text+effect-typewriter-cursor.md
Run the combined recipe in ONE render, never the four separately. Per-effect details: effect-marker-sweep.md, effect-active-word-box.md, effect-extruded-text.md, effect-typewriter-cursor.md under https://apihub.co.il/skills/.

## Plan
1. Get the video: Drive/Loom/Zoom link -> download the ORIGINAL; upload via POST /v1/studio/uploads (never a resized proxy). Check GET /v1/studio/probe. Keep the source orientation: landscape tutorials stay 16:9 (do NOT crop to 9:16); vertical stays 9:16.
2. Pace (what worked on the Loom tutorials): trim ONLY dead segments (POST /v1/studio/remove-silence, or cut long silences by transcript), plus a light global speed-up of ~7% so the pace is relatively high. Keep every explanation; never cut content.
3. Music: pleasant, light background music under the explanations, ducked well under the voice (~20dB+ below). Price before generating. Vary style between videos.
4. One render: POST /v1/studio/edit with video_url, language_code he, effects:
   - marker-sweep {y:17, text:<from speech>} start 0.3 dur 3.5
   - active-word-box {position:center}
   - extruded-text {y:58} start 1.3 dur 1.8
   - typewriter-cursor {y:17, text:<from speech>} start 0.1 dur 3.8
   audio {normalize:true, denoise}; output {aspect_ratio = source orientation, resolution per source, quality high}.
   Place start/duration on moments the words call for. Texts ONLY from what is actually said.
5. Always: header X-Tag per video, Idempotency-Key <tag>-<step>, price first via POST .../estimate, x-wait-ms 110000 then poll GET /v1/executions/{id}.
6. Check after render: captions cover all the speech (Loom #2 lost ~195 words and a 13s stretch — verify no gaps, and proper names are present).
7. Report: output.url (expires in 24h, download now) and cost via GET /v1/usage?tag=<tag>.

## Delivery
Upload the MP4 to your review Drive folder (<YOUR_REVIEW_FOLDER>) and a copy to your "ready" folder (<YOUR_READY_FOLDER>). No publishing. Then your ops bot sends the owner a WhatsApp with the link (<OWNER_WHATSAPP>), noting it is not published.
Standing rules: use only your APIhub key from a secret (e.g. APIHUB_API_KEY); never compress/squash the original; set a cost cap per video (estimate to the owner above it); no publishing unless the owner approves.

