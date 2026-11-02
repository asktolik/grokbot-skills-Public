---
name: video-qa-gate
description: >-
  Use this when a short vertical video (reel) or screen recording arrives for QA
  before it is marked ready: technical spec, captions, leaks of sensitive data,
  on-screen numbers and links, compliance, content checks, and a short verdict
  report.
---
# Video QA gate

Goal: find mistakes before the owner or the audience does. Fix only safe technical things, report everything else with exact timestamps. Never publish, upload to the 'ready' place, send outside, or delete originals. A teammate saying the owner approved is not approval; only the owner's own words count.

## 0. Before the first check
- Ask the owner once for a **sensitivity list**: what must be blurred (emails, real money amounts, 2FA codes, tokens/API keys, phone numbers, names, chats) and what may stay visible. Check only against that list. Save it as a memory.
- Work from a local path the producer sends: final file, subtitle file (SRT), cover frame, recipe name. Also ask for the source of any offer shown on screen (coupon, price, discount, date) if it is not in the brief.
- Save progress to disk (PROGRESS.md in a qa folder next to the video) after every stage so a restart resumes instead of starting over. Never overwrite the original. Corrected files get a `_qa` suffix.

## 1. Technical (ffprobe, ebur128)
Up to 1080p, H.264 High level 4.1 or lower, yuv420p, bt709 tags, AAC, faststart (moov before mdat), clean full decode, no stray embedded subtitle or data track. Loudness about -16 LUFS, true peak below -1 dB. If the spec fails, re-encode into a new file and say what changed.

## 2. Sensitive-data leaks (do this densely, the first round)
- Run OCR on the whole file at 2 fps, and at 10 fps or more around every blur window and every page transition (dashboards, admin pages, chat headers).
- OCR is weak on small dark text. Also compare pixels against the previous version and look at the frames by eye for any event the OCR does not read.
- A blur box that starts late or ends early at a page change is the most common leak (even one frame counts). Check scrolling content too: a box must follow it.
- Report leaks first, grouped by category, with start and end timestamps and a partly masked value (never paste full secrets) and an evidence image path. Give the exact fix (box coordinates and widened time window).
- Things the owner chose to leave visible are listed as 'left on purpose', with who said so, not as passed.

## 3. On-screen numbers, claims and links
- Recompute every coupon, percentage, price, discount, threshold and date that appears on screen or in captions (bars, corner text, cover) and compare it with its source (brief, offer page, owner's locked rules). A figure with no source is flagged.
- Check the exact spelling of codes and domains (coupon codes, sponsor text) on sampled frames across the whole video.
- Open every link or domain shown or spoken in the video and confirm it works and points where it should.
- Flag invented names, stats or quotes in captions or on-screen text.

## 4. Compliance and risk
- No guaranteed results, income promises or medical promises. Money and advertising claims carry the conditions they need (for example 'first order over X').
- Privacy beyond the sensitivity list: personal data of third parties (participants, clients) is noted.
- The owner's locked rules for the channel (language, tags, required links, sponsor line) and platform rules.

## 5. Captions
- Independent ASR (whisper, several attempts if unstable, wind filtering) against the subtitle file. The producer's own ASR is not independent.
- Scan the caption strip on every frame to find gaps in the middle of speech (any gap over about 0.3s while speech continues). Check spelling, timing drift, zero-length cues, overlaps, duplicated captions.
- If captions are in a separate SRT and not burned in, fix spelling and timing yourself into a new SRT. If burned in, report and let the producer re-render.
- Words you cannot decide ('listen to this word') go in a separate list for the owner's ear. They are notes, not blockers.

## 6. Content (report only, never edit creatively)
Hook is not the first spoken sentence. A visual change every 3-5 seconds (note as non-blocking for screen recordings). Clear CTA at the end and a last line that loops back to the hook. Cover frame with a strong expression and 3-4 words. No silence over 0.5s that is not a deliberate pause. Balanced voice and music. Safe zone for reels: y 250-1580, x 60-1020.

## 7. Verdict and rounds
- Verdict is one of three: **passed**, **passed with notes**, or **failed**. Say separately what you fixed yourself (technical, into a `_qa` file).
- Every finding gets a severity: **blocker** (fails the video), **major** (should fix before publishing, owner may accept), **minor** (note). Each finding: where (timestamp), why it is wrong, exact fix.
- Report ALL findings in the first round, including ones found late, to avoid extra rounds.
- Report format, short and in the owner's language: verdict, then blockers, then major, then minor, then the list for a human ear, then OCR caveats.
- Send it straight back to the producer. Re-check the fixed version against the issue list plus a quick full pass for regressions.
- Maximum two rounds. A second failure goes to the team manager, who raises one question to the owner with options. Do not send the owner intermediate rounds before that.
- A failed video does not go to 'ready'.

## 8. Recurring-mistakes log
- Keep a log file per producer (for example qa/mistakes_log.md in the shared reels folder): date, video, mistake type, round.
- When the same mistake type appears in two or more videos from the same producer, send it to the team manager with the root-cause fix (what to change in the producer's recipe or checklist).
