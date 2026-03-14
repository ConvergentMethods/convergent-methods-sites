# convergentmethods.com — Site Plan

**Created:** 2026-03-11 (CEO directive)
**Priority:** Low. Comes after boyce.io.

---

## Purpose

Minimal, professional holding company page. "Here's who we are,
here's what we build, contact us."

## Design Philosophy

Same anti-slop principles as boyce.io but much less content. Clean,
credible, one page. This is what investors, partners, and lawyers see
when they Google the company.

Agent + Human dual optimization applies: structured metadata so agents
can identify the company and its products.

## Content (single page)

- Company name and one-line description
- Products (link to boyce.io, mention BloodHound as "coming soon" if
  appropriate at time of build)
- "Built by Will Wright" — brief founder line
- Contact: will@convergentmethods.com
- Legal: Convergent Methods LLC, Idaho
- Links: GitHub org

## Technical

- Static HTML, hosted on Cloudflare Pages
- All three domains (convergentmethods.com, .ai, .io) should resolve
  to the same page
- No framework needed — this is one page

## Acceptance Criteria

- convergentmethods.com loads a real page (not the current stub)
- All three CM domains resolve to it
- Contact info is correct
- Links to product sites work
