---
name: site-audit
description: >-
  Use this when auditing a website for SEO, content, speed, accessibility, CRO
  or schema, or producing a monthly audit diff with scored P0/P1/P2 findings and
  evidence.
---
# Site audit

Scope: one production site, homepage, nav top pages, one page per public template, about 30 pages max. Gentle crawl, public pages only. Never change the live site.

## Checklist
1. SEO technical: status codes and redirect chains, robots.txt, XML sitemap matching live URLs, canonicals, noindex misuse, unique title (30-60 chars) and meta description, one H1, heading order, lang/hreflang, broken internal links, orphan pages, URL hygiene, HTTPS and mixed content, mobile viewport.
2. Content: page intent and target keyword match, thin or duplicate pages, value prop above the fold, readability, freshness, internal links between related pages, descriptive alt text, E-E-A-T (author, about, contact).
3. Speed: PageSpeed Insights / Lighthouse mobile and desktop (LCP, INP, CLS, TBT), CrUX field data if available, images, render-blocking JS/CSS, caching, fonts. Anything not measured is marked unmeasured with the reason.
4. Accessibility: contrast, alt text, form labels, keyboard focus and order, ARIA misuse, link text, lang, zoom and tap targets.
5. CRO: one clear primary CTA, CTA above the fold, form friction, trust signals, pricing clarity, contact/WhatsApp reachability, mobile usability, path to goal.
6. Schema: valid JSON-LD (Organization, WebSite, BreadcrumbList, Product/Course/Article/FAQ as fits), checked in Rich Results Test, matches visible content.

## Scoring
Each area 0-100 = 100 minus deductions (P0 -15, P1 -7, P2 -2, floor 0). Overall = average of measured areas only. Lab scores reported as-is, never estimated.

## Priority
- P0: blocks indexing, conversion or access now. Fix this week.
- P1: clear measurable loss (titles, Core Web Vitals, weak CTA, invalid schema, broken links). Fix this month.
- P2: polish. Backlog.
Every finding: issue, evidence URL (screenshot or tool link), why it matters, concrete fix, owner.

## Monthly diff
Same scope as baseline. Sections: Fixed (only with evidence), Still open, New, Regressions, score change per area. Update baseline snapshots (titles, HTML hashes). Report monthly even with no change.

## Tools
Direct HTTP fetch, PageSpeed Insights/Lighthouse, Rich Results Test / schema validator, Ubersuggest site_audit and pagespeed_audit as a second source, screenshots. Never invent traffic, rankings or conversion rates.

## Report
reports/YYYY-MM-DD.md and -diff.md, copied to latest.md: summary with overall and 6 area scores and top 5 fixes; P0, P1, P2 lists with evidence; per-area detail; unmeasured items and why; crawl scope and date. Evidence under evidence/YYYY-MM-DD/.
