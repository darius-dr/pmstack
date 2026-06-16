---
name: ingest-context
description: How to read a marketing-adjacent repo (PRD, DESIGN, REDESIGN-PLAN, TODOS, planning artifacts) without missing anything. Use when scanning an unfamiliar site repo for positioning context.
---

# Ingest-context

This skill teaches a pmstack subagent how to read a marketing-adjacent repo efficiently. Every pmstack run starts here.

## Files to look for (priority order)

### Tier 1 — read first, always
- `README.md` — project pitch, often has positioning hints.
- `CLAUDE.md` / `claude.md` — engineering project doc; usually has the most-current product description.
- `DESIGN.md` / `DESIGN_SYSTEM.md` / `BRAND.md` — design system + voice + tokens.
- `REDESIGN-PLAN.md` / `REDESIGN.md` / similar — most recent positioning rethink. Often has the cleanest current positioning.
- `TODOS.md` — surface area for known debts (legal flags, fake testimonials, broken claims).

### Tier 2 — read if present
- `docs/PRD.md` / `docs/PRODUCT.md` — formal product requirements.
- `docs/*.md` — all docs.
- `.planning/PROJECT.md` — overview.
- `.planning/STATE.md` — current focus.
- `.planning/ROADMAP.md` — what's shipped vs planned.
- `.planning/intel/SYNTHESIS.md` — pre-synthesized context.
- `.planning/intel/context.md` — problem framing.
- `.planning/intel/decisions.md` — locked decisions.
- `.planning/notes/*.md` — design + product notes.
- `.planning/seeds/*.md` — future-state thinking.
- `.planning/research/*.md` — what they've learned about the market.

### Tier 3 — read on `--full` only
- `.planning/phases/**/*.md` — phase logs (high volume, low signal for marketing).
- `.planning/todos/**/*.md` — task lists.

### Tier 4 — skip entirely
- `node_modules/**/*.md`
- `.next/**/*.md`
- `.git/**/*.md`
- `.claude/worktrees/**/*.md`
- `_archive/**/*.md`
- `test-results/**/*.md`

## Signals to extract

For every Tier 1-2 file, scan for these signals and note them with file paths:

### Brand + naming
- Product name (current).
- Legacy names (the PRD might use an old product name while the site uses the current one).
- Aesthetic name (e.g. "Calm Utility", "Editorial Bold").
- Voice + tone notes.

### Positioning
- One-line tagline / strategic line / north-star.
- "Memorable thing" (what people should remember).
- Value pillars.
- Differentiation vs competitors.

### Audiences
- Every named segment with its JTBD if present.
- Whether each segment has real proof (testimonials, pilots, named partners) or not.

### Stance
- Advisory stance: recommendatory ("you should buy this") vs interpretive ("here are the facts, you decide").
- Banned phrases / verbs.
- Honesty commitments (e.g. "no coming-soon tags").

### Shipped vs aspirational
- Features marked DONE / shipped vs PLANNED / 🔜 / future.
- Capabilities the site claims that the product doesn't deliver yet.
- LEGAL TODOs that constrain copy.

### Operational
- Geography + language(s).
- Pricing — current, whether it's stale, B2B vs B2C.
- Data sources / partners (real ones that can be cited).
- Tech stack (informs editing format for /pm:ship).

### Design tokens
- Color palette + token names.
- Typography stack.
- Spacing scale.
- Motion durations + easings.
- Signature visual device.

## How to handle conflicts

Marketing-adjacent repos often have contradictory MDs because different sessions update different files. When you find conflicts:

1. **Newer wins by default.** Check `git log` if available; otherwise file mtime.
2. **REDESIGN-PLAN.md beats PRD.md for current positioning** — PRDs go stale fast.
3. **DESIGN.md beats inline comments** for visual/voice questions.
4. **Legal TODOs beat marketing aspirations** for copy honesty.
5. **Always surface unresolved conflicts in the positioning brief** under a "Conflicts" heading — don't silently pick a side.

## How to handle missing context

If a critical piece is missing (e.g. no DESIGN.md, no documented banned-verb list):
- Note it in the positioning brief as a gap.
- Use general best-practice defaults.
- Surface the gap in the chat summary so the user can fill it.

Never invent a brand voice or a banned-verb list. Read or ask.

## What NOT to do

- Don't read code files. Code is for /pm:visual-critique to consult later. Ingest is doc-only.
- Don't read CHANGELOG, RELEASE-NOTES, dependency-update MDs — too low-signal.
- Don't summarize PRD prose; extract structured signals.
- Don't infer audiences that aren't named in the docs.
