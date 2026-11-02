---
name: routine-healthcheck
description: >-
  Use this when the Monday routine-healthcheck fires, or when auditing fleet
  routines for dead schedules, policy conflicts, or token waste.
---
# routine-healthcheck

Monday audit of fleet routines for waste and policy drift. Run as a recipe; the routine owns the schedule and delivery.

## Rules
- Propose only; never pause/edit/delete another bot’s routine until the owner picks.
- Stay quiet when nothing is worth proposing.
- Prefer pause/disable or prompt rewrite over new bots.
- Respect the owner's standing locks (e.g. paused bots stay paused until the owner re-enables them; the approved tool stack; the token-savings skill).

## Steps
1. Gather routine configs you can see: this bot’s server routines, plus other agents’ `automations/*/automation.json` on the box, and any gateway/listAllAutomations signal if available.
2. Flag: enabled-but-dead (`lastRun`/`nextRun` stuck), schedule vs policy conflict, noisy empty wakes, obsolete tools/names in prompts, duplicates.
3. Skip unverifiable cloud-only routines with no lastRun signal rather than inventing waste.
4. Hand back to the parent a short list for the owner, in the owner's language: each item = bot | routine name | problem | proposed fix. Parent delivers; this skill does not message the user.
