---
name: Inbox triage
description: >-
  Use this to rank the owner's unread email by urgency and save reply drafts for
  review, never sending.
---
# Inbox triage

1. Search unread inbox mail from the last ~7 days (e.g. `is:unread in:inbox newer_than:7d`, up to ~50 messages) with the Gmail connector.
2. Read the important ones. Count promotions and newsletters but leave them out of the ranking.
3. Rank into tiers: urgent, today, this week, FYI. Use the sender, deadlines, asks directed at the owner, money or legal signals, and people waiting on a reply.
4. For each message that needs a reply, write a short draft in the original email's language, in the owner's voice. Save it only as a Gmail draft (create_draft with replyToMessageId).
5. Never send, archive, label, or delete mail.
6. Report a compact ranked list: sender, subject, one-line reason, tier, and whether a draft was saved, plus the count of skipped promotional mail.
