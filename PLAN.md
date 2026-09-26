# convergentmethods.com — Site Plan

**Created:** 2026-03-11 (CEO directive)
**Historical launch:** 2026-03-13.
**Current web-presence source of truth:** `ops/web-presence/README.md` in the
main ConvergentMethods repository. This plan is historical content direction,
not an independent hosting or deployment runbook.
**Current host (verified 2026-09-25):** Cloudflare Pages project
`convergent-methods-sites.pages.dev`, serving `convergentmethods.com`.
GitHub Pages also serves a separate project-path copy. Authenticated Cloudflare
settings confirm automatic production deployments from this repository's
`main` branch. Verify deployment success and the custom domain after a push.
**Content status:** The live homepage and Boyce pages still represent the
pre-2026-06-12 AI/developer-tools focus. Convergent Methods now builds games;
the public site needs a founder-directed revision. Boyce is legacy/archived.

---

The original March 2026 brief below is retained as launch history, not as a
current redesign specification. New content must follow the game-development
focus above.

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
- Products (link to boyce.io)
- "Built by Will Wright" — brief founder line
- Contact: will@convergentmethods.com
- Legal: Convergent Methods LLC, Idaho
- Links: GitHub org

## Technical

- Static HTML, hosted on Cloudflare Pages
- `convergentmethods.ai` and `.io` redirect to the `.com` homepage
- `boyce.io` redirects to the legacy `/boyce/` page
- No framework needed — this is one page

## Acceptance Criteria

- convergentmethods.com loads a real page (not the current stub)
- All three CM domains resolve to it
- Contact info is correct
- Links to product sites work
