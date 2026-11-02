---
name: transcript-healthcheck
description: >-
  Use this when the weekday transcript-healthcheck routine fires, or when
  auditing fleet chat friction from box transcript mirrors.
---
# transcript-healthcheck

Standing weekday scan for fleet conversation friction. Run as a recipe; the routine owns the schedule and delivery.

## Rules
- Window = since last successful run of this check (fallback: last 24h).
- Propose only `skill` | `bot` | `routine` (or a clear data-gap). Never auto-create or edit bots/skills/routines from the report.
- Stay quiet when there is nothing useful to propose and the data source is healthy.
- Do not fan out miners to other bots; scan on this box only.

## Steps
1. List non-`sand-subagent-` dirs under `/home/box/agent-data/agent-transcripts`. Note mtimes and any jsonl/store activity inside the window.
2. Optionally check `transcript_entries` / local store ages the same way if present.
3. **Data-gap branch (required):** if mirrors/store are older than the window, or core live bots (team manager, ops, publisher, editors) lack a transcript dir while shared memory shows recent work — report that as friction instead of a silent “all clear.”
4. If there is mineable chat text in-window, extract real friction (duplication, stuck handoffs, unclear ownership, broken SOPs). Skip noise and one-off banter.
5. Hand back to the parent a short note for the owner, in the owner's language: empty / friction / data-gap, plus at most a few pick-before-create proposals. Parent delivers; this skill does not message the user.
