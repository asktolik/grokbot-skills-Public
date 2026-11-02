---
name: bar-shaltiel
description: >-
  Edit a talking-head reel in the "בר שלתיאל" style: 9:16 split screen with the
  face on top and a fast-changing B-roll/screenshot panel below, 1–3 word bold
  captions at the seam with colored keyword pops, pinned title-box hook, flashes
  and number cards, social CTA end. Use only when explicitly requested by name.
---
# בר שלתיאל: style recipe

Use only on explicit request. Estimate before any paid step; stop and report over 500 credits.

## Style anatomy
- **Aspect:** keep the original (refs are 9:16).
- **Layout:** the face fills the top ~58%. The bottom ~42% panel is almost always filled with AI images, stock clips or screen recordings, changing every 1.5–2.5 s. Go full-frame face for short breathers and in the outro.
- **Hook (0–4 s):** a pinned 2–3 line title box at top center (purple or magenta). Its text is a line the speaker actually says. Big FX hit on the first frame, and a hero visual in the panel.
- **Captions:** 1–3 words, white extra bold with a dark shadow, at the seam. Keywords pop as one big colored word with a scale-in.
- **Voice:** tight jump cuts with no dead air, and the voice stays continuous.
- **FX:** full-frame color flashes on key words, sticker or emoji pops, red arrows or boxes on screen recordings, big step numbers over a dimmed face. Never blur.
- **Ending:** full-frame face with Follow, comment and share icon pops. CTA text only if it's spoken.

## Steps (API Hub Studio + local ffmpeg)
1. Probe the source and keep its size and rotation. Upload it with `POST /v1/studio/uploads`, then transcribe (he) with `POST /v1/speech/transcripts` plus local Whisper medium. Merge the two and mark disagreements [?]. Get the captions proofread; hide anything unclear and never guess.
2. Hook: pick a 2–4 s spoken line. It becomes the title box (local ASS, Heebo Black, purple #7B3FF2 box, white text).
3. `POST /v1/studio/kinetic` with `cut:{from:"audio",min_pause_ms:200,padding_ms:70}`, keyword emphasis, punch zooms on about 1 in 6 key words, and stickers from `/v1/stock/icon`. Get whoosh, pop and riser from `POST /v1/ai/sound-effects`.
4. Panel: `POST /v1/stock/broll-plan` with `style:"cutaways"`, mode split (face on top), 8–12 shots per ~90 s. Place screen recordings locally in the lower 42%, with red arrows or boxes drawn via drawbox.
5. Render once with `POST /v1/studio/edit` with `texts:[]` and no Hub music. Use only the video stream.
6. Captions as local ASS: Heebo Black, white with a 4px outline and shadow, 1–3 words per card at y≈58%. A keyword is one word at 130% in #8A4DFF or #E0218A with a 120 ms pop. For RTL, order the runs [after][hl][before].
7. FX locally: full-frame color flash at alpha 0.35 for 0.3 s on 2–4 moments. Number cards are PNGs over a dimmed face (`eq=brightness=-0.25`), never boxblur.
8. Music from `/v1/ai/music` (light upbeat instrumental) or a free bed. Keep it constant about 21 dB under the voice, `amix normalize=0`, no ducking, 2 s fade-out. Master at about -14 LUFS.
9. End: last ~6 s full-frame face with follow, comment and share icon pops plus pop SFX.
10. Export H.264 High, yuv420p, AAC, +faststart, original WxH and rotation, under 100MB. QA: sync, continuous voice, aspect ratio, no blur, MP4 plays. Deliver for review; don't publish.

Rough cost for ~90 s: about 190 credits (render price unconfirmed). Always run the edit estimate first.
