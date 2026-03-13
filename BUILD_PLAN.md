# convergentmethods.com + /boyce — Build Plan

**Created:** 2026-03-13
**Author:** CTO (Opus planning pass)
**Executor:** Sonnet · medium
**Status:** AWAITING APPROVAL

---

## Context

boyce.io DNS is blocked (Dynadot PIN lockout). The Boyce product page will deploy as `convergentmethods.com/boyce/` via GitHub Pages until boyce.io is independently live. This build also replaces the convergentmethods.com stub with a real holding company page.

**Repo:** `ConvergentMethods/convergent-methods-sites` (GitHub Pages, already deployed)
**Current state:** Single `index.html` stub with dark background and "coming soon" text.

---

## Design Constraints

### Do
- Dark theme, high contrast, clean typography
- System font stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif`
- Monospace for all code: `"SF Mono", "Fira Code", "Fira Mono", Menlo, Consolas, monospace`
- Code-forward: real examples, real output, real config blocks
- Mobile responsive from the start
- Prism.js from CDN for syntax highlighting (dark theme, e.g. `prism-tomorrow`)
- Agent + human dual optimization: clean semantic HTML, structured metadata (OpenGraph, JSON-LD)
- Fast: no web fonts to download, no frameworks, no build step. Target <100ms load.

### Do Not
- No gradients, no animations, no parallax, no hero videos
- No "Trusted by" logos, no testimonials, no social proof (we have none yet)
- No pricing tables (it's MIT/free)
- No team page, no "About Us" beyond a founder line
- No newsletter signup (premature)
- No "Request a demo" or "Book a call" CTAs
- No AI slop language: no "revolutionize", no "game-changing", no "next-generation"
- No emojis in headings or body copy (emojis OK in the three-layer table as they're in the README)
- No framework: no React, no Tailwind, no build tooling

### Color Palette
- Background: `#0d1117` (GitHub-dark range — not pure black)
- Surface/card: `#161b22`
- Border: `#30363d`
- Primary text: `#e6edf3`
- Secondary text: `#8b949e`
- Accent (links, highlights): `#58a6ff` (restrained blue — not startup cyan)
- Code background: `#1c2128`
- Success/green accents (sparingly): `#3fb950`

These are in the GitHub dark palette range. Familiar to developers, easy on the eyes, zero "look at our brand" energy.

---

## File Structure After Build

```
convergent-methods-sites/
├── index.html              ← Convergent Methods holding company page
├── styles.css              ← Shared stylesheet (both pages)
├── boyce/
│   └── index.html          ← Boyce product landing page
├── CNAME                   ← convergentmethods.com (may already exist in repo)
├── CLAUDE.md
├── PLAN.md
├── BUILD_PLAN.md           ← This file
└── README.md
```

---

## Build Steps

### Step 1: Shared Stylesheet (`styles.css`)

Create `styles.css` at repo root. Both pages link to it.

**Contents:**
- CSS reset (minimal — box-sizing, margin, padding)
- Root variables for the color palette
- Base typography: system font stack, sizes, line heights
- Layout: max-width container (720px for prose, 960px for code-heavy sections), centered
- Code blocks: monospace, dark background, rounded corners, horizontal scroll on overflow
- Responsive breakpoints: single breakpoint at 768px (stack layout on mobile)
- Utility classes: `.mono`, `.muted`, `.accent`
- Nav: minimal top bar with logo text + links
- Footer: muted, small, centered
- Table styling: clean borders, alternating row backgrounds (subtle)
- Tab component: for install instructions (pure CSS + minimal JS)

**No Prism.js in Step 1.** Get the structure right first, add syntax highlighting last.

### Step 2: Convergent Methods Root Page (`index.html`)

Replace the stub. Single-page holding company site.

**Sections in order:**

1. **Header/Nav**
   - "Convergent Methods" (text, not a logo image)
   - Link to GitHub org: github.com/ConvergentMethods

2. **Hero**
   - Company name: "Convergent Methods"
   - One-liner: "AI-native developer tools. Open protocols. MIT licensed."
   - No tagline beyond this. No "We believe" statements.

3. **Products**
   - **Boyce** — one paragraph description + link to `/boyce/`
     - "Semantic protocol and safety layer for agentic database workflows. Gives AI agents the structured database intelligence they need to generate correct, safe SQL — deterministically."
     - `pip install boyce` shown inline
     - Links: `/boyce/`, GitHub, PyPI
   - **BloodHound** — one line only, if Will approves including it
     - "Cross-domain value-leak detection. Early stage."
     - No link (nothing to link to yet)

4. **About**
   - "Built by Will Wright. Based in Idaho."
   - No photo, no bio paragraph. Just the line.

5. **Footer**
   - Contact: will@convergentmethods.com
   - Legal: "Convergent Methods LLC. MIT licensed."
   - GitHub: github.com/ConvergentMethods
   - Copyright line

**Metadata:**
- `<title>`: "Convergent Methods — AI-native developer tools"
- OpenGraph tags: title, description, url
- `<meta name="description">`: "Open-source developer tools for agentic database workflows. Built by Convergent Methods."
- Structured data (JSON-LD): Organization schema with name, url, founder, product references

### Step 3: Boyce Product Page (`boyce/index.html`)

The main deliverable. Single-page product landing.

**Sections in order:**

#### 3a. Header/Nav
- "Boyce" (text) — links to this page
- "Convergent Methods" — links back to root `/`
- GitHub link

#### 3b. Hero
- Tagline: **"Don't let your agents guess. Give them Eyes."**
- One-sentence explainer: "Semantic protocol and safety layer for agentic database workflows."
- Install block (prominent, styled as a terminal):
  ```
  pip install boyce
  ```
- Secondary links: GitHub | PyPI | Docs

#### 3c. The Problem (3-4 sentences)
- AI agents querying databases without context generate unreliable SQL
- They work from incomplete schemas, guess join paths, miss NULL distributions
- A naive equality filter on a column with 30% NULLs silently drops rows — and the agent never knows
- "Boyce gives agents structured database intelligence so this doesn't happen."

#### 3d. The Three Layers (table or cards)

| Layer | What it does |
|-------|-------------|
| **The Brain** | NL → StructuredFilter → deterministic SQL. Same inputs, same SQL, byte-for-byte, every time. Zero LLM in the SQL compiler. |
| **The Eyes** | Live Postgres/Redshift adapter. Your agent sees real schema, real data distributions, real NULL rates before writing a single filter. |
| **The Nervous System** | EXPLAIN pre-flight on every generated query. Bad SQL is caught at planning time — not at 2am in your on-call rotation. |

#### 3e. How It Works (two paths)

**Path 1 — MCP Hosts (no API key needed)**
Show the actual JSON config for Claude Desktop/Cursor. Explain: your host's LLM calls `get_schema`, reasons over the schema, calls `build_sql`. Boyce compiles deterministic SQL with zero LLM calls.

```json
{
  "mcpServers": {
    "boyce": {
      "command": "boyce",
      "env": {
        "BOYCE_DB_URL": "postgresql://user:pass@host:5432/db"
      }
    }
  }
}
```

**Path 2 — CLI / HTTP / Non-MCP**
Show config with `BOYCE_PROVIDER` + `BOYCE_MODEL`. One-liner: "Boyce uses LiteLLM — supports Anthropic, OpenAI, Ollama, and 100+ providers."

#### 3f. MCP Tools (table)

The 8 tools table from the README. Clean, scannable.

| Tool | Purpose |
|------|---------|
| `ingest_source` | Parse a SemanticSnapshot from dbt, LookML, DDL, SQLite, Django, SQLAlchemy, Prisma, CSV, or Parquet |
| `get_schema` | Return full schema context — host LLM uses this to construct queries without a Boyce API key |
| `build_sql` | Compile a StructuredFilter to SQL — deterministic, no LLM call |
| `ask_boyce` | Full NL → SQL pipeline with NULL trap detection and EXPLAIN pre-flight |
| `query_database` | Execute read-only SELECT against live database |
| `profile_data` | Null %, distinct count, min/max for any column |
| `solve_path` | Optimal join path between entities via Dijkstra |
| `ingest_definition` | Store certified business definitions — auto-injected at query time |

#### 3g. What It Parses (parser list)

Show the 10 parsers as a clean grid or list. This signals maturity.

"Point Boyce at your project. It figures out what you have."

```bash
boyce-scan ./my-project/
```

dbt manifest | dbt project | LookML | Raw DDL | SQLite | Django | SQLAlchemy | Prisma | CSV | Parquet

#### 3h. Architecture Diagram

The ASCII flow diagram from the README, rendered in a styled code block:

```
SemanticSnapshot (JSON)
        │
        ▼  ingest_source
  ┌─────────────────────────────────┐
  │     SemanticGraph (NetworkX)    │
  │  entities → weighted joins     │
  └─────────────────────────────────┘
        │                    │
        ▼  ask_boyce         ▼  solve_path
   QueryPlanner          Dijkstra
   (LiteLLM)             join resolver
        │                    │
        └────────┬───────────┘
                 ▼
        kernel.process_request()    ← ZERO LLM
        SQLBuilder (dialect-aware)
                 │
                 ▼
        EXPLAIN pre-flight          ← safety layer
                 │
                 ▼
         SQL + validation result
```

Dialect support: Redshift, Postgres, DuckDB, BigQuery

#### 3i. Quick Start

Compact 4-step flow:

1. `pip install boyce`
2. `boyce-init` (auto-detects your MCP host)
3. Point at your project: `boyce-scan ./my-project/`
4. Ask: `boyce ask "total revenue by customer segment"`

#### 3j. Footer
- Named for Raymond F. Boyce, co-inventor of SQL (1974)
- Links: GitHub | PyPI | Troubleshooting
- "Built by Convergent Methods" — links to root
- MIT License | Copyright 2026

**Metadata:**
- `<title>`: "Boyce — Semantic Protocol & Safety Layer for Agentic SQL"
- OpenGraph: title, description, url (convergentmethods.com/boyce)
- `<meta name="description">`: "Give AI agents structured database intelligence. Deterministic SQL compiler, NULL trap detection, EXPLAIN pre-flight. MIT licensed. pip install boyce."
- JSON-LD: SoftwareApplication schema with name, description, url, applicationCategory, operatingSystem, offers (free)

### Step 4: Syntax Highlighting

Add Prism.js (tomorrow-night theme) from CDN. Apply to all `<code>` blocks on the Boyce page. JSON, bash, SQL, and Python language support.

Two `<script>` tags and one `<link>` in the `<head>`. No local files.

### Step 5: CNAME File

Verify or create `CNAME` file at repo root containing:
```
convergentmethods.com
```

If it already exists in the repo, leave it. If not, create it — GitHub Pages needs this for custom domain routing.

### Step 6: Verify and Push

- Check both pages render correctly in a browser (open local files)
- Verify mobile layout at 375px width
- Verify all links point to correct destinations
- Verify code blocks render with proper highlighting
- Push to `main` branch → GitHub Pages deploys automatically

---

## Content That Must Come From Will (or Needs Approval)

1. **BloodHound mention:** Include on CM page or omit?
2. **Founder line wording:** "Built by Will Wright" — or something different?
3. **Contact email:** `will@convergentmethods.com` is listed in PLAN.md. Confirmed?
4. **The Problem section wording:** The 3-4 sentences in section 3c — Will should review for tone
5. **Any additional links:** Twitter/X? LinkedIn? Or keep it minimal?

---

## What This Plan Does NOT Cover

- boyce.io independent deployment (blocked on Dynadot — see `reference_domain.md`)
- Null Trap essay (separate content piece, future addition)
- Blog section (added with first essay)
- MCP directory submissions (need live URL first — this build gives us one)
- Email DNS setup (separate infra task)
- Analytics/telemetry (CEO decision pending)

---

## Acceptance Criteria

- [ ] convergentmethods.com shows a real holding company page (not stub)
- [ ] convergentmethods.com/boyce/ shows the Boyce product page
- [ ] Both pages share a stylesheet and visual identity
- [ ] Both pages are mobile responsive
- [ ] All code blocks have syntax highlighting
- [ ] All links are valid (GitHub, PyPI, cross-links between pages)
- [ ] Page loads in <200ms on a cold cache
- [ ] Semantic HTML: proper heading hierarchy, nav, main, footer
- [ ] OpenGraph + JSON-LD metadata on both pages
- [ ] No AI slop language anywhere
- [ ] Pushed to main, live on GitHub Pages
