# convergentmethods.com

Public website source for Convergent Methods LLC. The live custom domain is
served by Cloudflare Pages, not GitHub Pages. This repository also has a
separate GitHub Pages copy at
`https://convergentmethods.github.io/convergent-methods-sites/`.

The published copy still describes the pre-2026-06-12 AI/developer-tools
business. Convergent Methods is now a game-development company; the site needs
a content and design revision before it accurately represents the company.

## Structure

```
index.html          ← Convergent Methods holding company page
styles.css          ← Shared stylesheet
llms.txt            ← Agent-readable company index (llmstxt.org spec)
boyce/
  index.html        ← Boyce product landing page
  llms.txt          ← Agent-readable Boyce index
  llms-full.txt     ← Complete Boyce agent reference
```

## Deployment

The current hosting/deployment source of truth is
`ConvergentMethods/convergent-methods-ceo/ops/web-presence/README.md` in the main CM
repository. As verified on 2026-09-25, `https://convergentmethods.com/` matches
the Cloudflare Pages project at `https://convergent-methods-sites.pages.dev/`.
**Do not assume a push to `main` updates the live custom domain:** the
Cloudflare Pages source trigger requires authenticated dashboard readback.

- **Registrar:** Namecheap; **DNS and live hosting:** Cloudflare
- **Redirects:** convergentmethods.ai and convergentmethods.io redirect to .com
- **HTTPS:** Served through Cloudflare on the live domain

## URLs

- https://convergentmethods.com — holding company page
- https://convergentmethods.com/boyce/ — Boyce product page
- https://convergentmethods.com/llms.txt — agent index
- https://convergentmethods.com/boyce/llms.txt — Boyce agent index
- https://convergentmethods.com/boyce/llms-full.txt — Boyce full agent docs

## Domain Portfolio

See `ops/web-presence/README.md` in the main ConvergentMethods repository for
the complete, current domain inventory and operating procedure.
