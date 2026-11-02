---
name: Broll
description: >-
  Use this as the DEFAULT video edit for the owner's uploaded raw videos when they
  name no other edit skill. "עריכה רגילה" (normal edit) means exactly the locked
  Default recipe below: hook cold open, local line cuts, one APIhub stock-broll
  render, local silence cut, speed and burned captions, continuous voice.
---
# Broll — APIhub full/stock-broll ("B-roll מסטוק במקום וידאו AI")
Recipe (public Markdown, fetch with GET): https://apihub.co.il/skills/full-stock-broll.md
Default edit when the owner names no other skill. A skill name the owner defines overrides it.

## Flow
1. Get the original recording (Drive link, or upload via POST /v1/studio/uploads). Never upload a squashed or resized proxy; check GET /v1/studio/probe?url=...
2. Open the recipe and follow its steps in order (remove-silence, transcript and kinetic plan, ai/text plan, sound effects, icons, ai/music, stock/broll-plan, studio/edit render).
3. Before any AI generation (music, images, voice) get the price (POST .../estimate) and tell the owner; wait for OK unless the owner already set a cap.
4. Headers: Authorization Bearer key, Content-Type JSON, X-Tag (one name per video), Idempotency-Key tag-step on every POST. Long calls: x-wait-ms 110000, then poll GET /v1/executions/{id} every 5 s.
5. Titles and on-screen text only from what is said; never invent facts. Verify Hebrew RTL captions.
6. Deliver: final link (output.url, expires in 24h, download immediately) and total cost from GET /v1/usage?tag=TAG (credits and estimated ILS).
Docs: https://apihub.co.il/docs · skills index https://apihub.co.il/skills/index.md

## Default recipe — "עריכה רגילה" (locked 2026-10-15)
When the owner says "עריכה רגילה" (normal edit), run exactly this. It overrides the plain Flow above where they differ.

### Rules
- Use only your APIhub key from a secret (e.g. `APIHUB_API_KEY`). Check it first with `GET /v1/me`. Never use any other key.
- Price before spending: get estimates (`POST /v1/studio/edit/estimate`, music ≈ 0.77 credits/s) and stop if the total is over the cap the owner set.
- Keep the original aspect ratio (check the rotation flag: a phone clip that is 3840x2160 with rotation 90 is 9:16 portrait). No blur. Never publish.
- On-screen text only from what was said. A proofreader bot checks the caption text before the render. An unclear word is checked with Whisper medium: if two sources agree, keep it; otherwise hide it. Never guess.
- **The voice plays continuously for the whole video.** It is never cut mid-word, ducked, muted or replaced, and there are no fades at joins.

### Steps
1. **Probe and transcribe.** Download the original (gdown) into `/workspace/reels/<job>/`, then ffprobe it (codec, size, rotation, duration). Upload the original to the Hub, transcribe it, and write the numbered caption lines to `captions.md`, with suspect words marked [?] and proposed [CUT] lines (repetition, garbled parts) marked to reach about 1:30. Pick a hook from the speaker's own words (one strong 2–4 s line). Get a price, then stop for proofreading and approval.
2. **Assemble locally (hook cold open + approved cuts).** Keep spans on the source clock: the hook first, then the body minus the [CUT] lines. Encode each span on its own with `ffmpeg -nostdin` (inside loops), accurate seek, H.264 CRF 14, yuv420p, the original resolution. **Add no audio filters (`afade` with a pre-roll seek mutes the end of the span; that was the 2026-10-15 bug).** Concat with `-c copy`. Use separate passes per span, not one filtergraph with many trims (4K runs out of memory).
3. **Rebuild the voice exactly on the frame clock.** Do not trust the concat's AAC track: it drifts about 0.04 s per join. From the original audio (WAV), place each span at its video offset, where the offset is the sum of round(dur×30)/30 over the earlier spans. At most a 10–15 ms click-guard ramp at each edge. That makes `voice_clean.wav`.
4. **One Hub render for the picture.** Upload the assembled file. Call `POST /v1/studio/kinetic` with `cut: false`, no speed and `resolution: "1080"` to get the zooms and flashes. Then `POST /v1/stock/broll-plan` (style cutaways, count 3, kind video, Pexels) with a whoosh. Set `texts: []`, remove the music, and set `audio.denoise: "light"`. Estimate, then render once with `POST /v1/studio/edit`. The render is not cut, so its clock equals the assembled clock. Use only its video stream.
5. **Captions.** Map the approved, proofread words (from the original transcript, with fixes applied) to the assembled clock, then through the keep spans and the speed. Burn in designed ASS captions: Heebo Black, cards of up to 3 words, the active word lime `#D0F808` at about 108%, the hook big at the top, strip trailing commas and periods. For Hebrew right-to-left text, write the runs as [after][highlight][before] or the order flips. Check a few frames visually.
6. **Silence cut and speed, locally.** Keep spans come from the word times (cut gaps over about 0.2 s, 70 ms padding). Use `select`/`aselect` with `between()` (one pass), then `setpts=.../1.08` and `atempo=1.08` (target about 1:30). Apply the same spans and speed to the video (the Hub render) and to `voice_clean.wav` (light afftdn and highpass, then `loudnorm` at -16 LUFS).
7. **Music.** A fresh `POST /v1/ai/music` track (light, instrumental), set to a constant -37 LUFS (about 21 dB under the voice), with `amix normalize=0`. No ducking and no sidechain. A 2 s fade-out at the end only. Check that the track is not silent; if it is, use the Hub's free CC0 bed.
8. **Mux.** The video encode (H.264 High, yuv420p, faststart; under 100 MB for UploadFile, so CRF about 19 with maxrate 8M) plus AAC 48k. When remixing audio, copy the video stream.
9. **Verify.**
   - ffprobe: codec, profile, size, pixel aspect ratio, duration. Check the aspect ratio and absence of blur on frames.
   - Whisper medium on the full final against the caption text: no missing lines.
   - Per-second voice RMS: no second near silence where there is speech.
   - Sync: anchor words from start to end, captions within 0.2 s of the audio.
10. **Deliver.** UploadFile to the מוכן folder, named after the hook (e.g. `הפחד הוא משינוי.mp4`). Check the parent folder, download it back, `cmp` against the local file, and decode it cleanly. Drive may label it application/mp4; report that. To replace an older version, trash it only after the new one is verified. Report the link, length and `GET /v1/usage?tag=` cost. Delete the raw and intermediates after delivery.

## Owner's standing additions to "עריכה רגילה" (locked 2026-10-18)
- Captions that look good and match the video's style; spelling proofread (proofreader bot) — zero errors.
- Cut silent/dead parts.
- Keep attention high even on longer videos: strong hook in the first seconds, zooms/highlights on key moments, tight pacing.
- Full QA before מוכן: sync, continuous voice, music ~21dB under (no ducking), original aspect ratio, no blur on screen recordings, standard MP4 that opens in Drive.
- **QA gate by the QA bot:** after your own QA, send the QA bot the local path, the proofed SRT, the cover frame and the recipe name. Upload to מוכן only after QA approves. Technical issues QA fixes itself; content issues return to you with timestamps. Maximum 2 rounds, then QA tells the team manager.
- **Only after QA approves** and the final is in מוכן: send the owner a WhatsApp via the ops bot that it's ready (with the Drive link). Without QA approval, no WhatsApp. No publishing.
