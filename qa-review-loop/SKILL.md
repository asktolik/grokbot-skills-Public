---
name: qa-review-loop
description: >-
  Use this when another bot sends you work to check before it ships (copy,
  pricing, maths, e-commerce, health claims, posts, code, data): review it, list
  risks, send fixes back, and loop until it passes.
---
# QA review loop

1. **Intake.** Note who sent it, what it is, where it will ship, the audience, and the deadline. If the source data or brief is missing, ask the sending bot for it before reviewing.
2. **Check, in order of cost of a mistake:**
   - **Maths and numbers:** recompute every total, percentage, price, discount, currency and date. Compare figures with their source; flag any number with no source.
   - **Facts and claims:** every claim must trace to a real source. Flag invented quotes, names, stats or links. Open links and confirm they work.
   - **Compliance and risk:** health, legal, financial and advertising claims (no guaranteed results, no medical promises, required disclaimers), privacy (no personal data exposed), platform rules, and the owner's locked rules for this channel.
   - **Brand and format:** language, tone, tags, hashtags, required links, and the exact format the owner locked.
   - **Function:** if it's a page, flow, code or automation, actually test it (run it, click through, try edge cases) rather than reading it.
3. **Verdict.** One of: PASS, PASS WITH NOTES, or FIX REQUIRED. For each issue give severity (blocker / major / minor), where it is, why it's wrong, and the exact fix.
4. **Send back** the verdict and fixes directly to the sending bot. Keep it short and actionable; don't rewrite their whole deliverable unless asked.
5. **Loop:** re-check only the fixed version against the issue list plus a quick full pass for regressions. Repeat until PASS.
6. **Escalate to the owner** only when a fix needs a decision only they can make (price, legal risk acceptance, brand change), or after two failed fix rounds. Give them the one question and the options.
7. **Log** recurring mistakes per bot so you can tell that bot (or the team manager) to fix the root cause.
