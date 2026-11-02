---
name: app-growth-report
description: >-
  Use this when asked for the daily or on-demand report on mobile app install
  campaigns (for example X ads) measured in Kochava: installs, clicks and
  conversions per campaign, comparison, short recommendations. Read-only by
  default; changes need the owner's explicit yes.
---
# App growth report (Kochava)

## Before you start
1. The Kochava connector (official remote MCP, https://analytics.mcp.kochava.com/mcp, header authentication-key) must be connected. Check with GetMcpServerStatus. If it is not connected or returns 401/403, stop and tell the owner what is missing. Never ask for or print the API key in chat.
2. List the connector's real tools with GetDynamicTools before the first call. Use only tools that exist. Never invent tool names, campaign names, numbers or results.

## Report (read-only)
1. For the requested period (default: yesterday vs the day before, and the last 7 days), pull per campaign and per network (focus: X): installs, clicks, conversions/events, and cost data if Kochava has it.
2. Compare campaigns: best and worst by installs and by conversion rate; flag a campaign whose installs fell or rose sharply versus its own recent days. A tiny sample is a signal, not a conclusion: say how few installs it is based on.
3. Write a short report in Hebrew: 3-5 lines of what changed, a small table (campaign, installs, clicks, conversions, change), and at most 3 concrete recommendations marked as suggestions.
4. Mark clearly what is data and what is your inference. If a number is missing or a tool fails, say so.

## Daily routine rule
Send the owner a message only when something is unusual (a sharp change, a broken tracker, zero installs where there were some) or a decision is needed. Otherwise stay quiet.

## Never without an explicit yes for that exact action
Creating or changing trackers, campaigns, segments, budgets or any delete. Create things paused. Never spend money or switch on a campaign on your own. Free-account signup tools at Kochava create an account and accept terms: only the owner decides that.

## Limits
Free Kochava accounts keep 30 days of data. Attribution counts can lag: say so when yesterday's numbers look low.
