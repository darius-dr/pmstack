---
description: Ingest all marketing-relevant MD context from the repo and produce a positioning brief + per-segment ICP scaffolds.
argument-hint: "[--full] (optional, include planning archives)"
allowed-tools: Read, Glob, Grep, Write
---

# /pm:ingest

You are running pmstack's ingest step. Your job is to read the marketing-relevant context that already exists in the repo, then produce two artifacts:

1. `.pmstack/positioning.md` — a single source of truth for the product's positioning (north-star tagline, audiences, value pillars, banned phrases, advisory stance).
2. `.pmstack/icp/{segment}.md` — one scaffold file per audience segment you find evidence of.

## Procedure

1. **Scan for marketing-relevant MDs**, ignoring `node_modules/`, `.next/`, `.git/`, `_archive/`, and `*.worktrees/`:
   - Root-level: `README.md`, `CLAUDE.md`, `claude.md`, `DESIGN.md`, `REDESIGN-PLAN.md`, `TODOS.md`, `LICENSE.md`.
   - Product docs: `docs/PRD.md`, `docs/**.md`.
   - Planning artifacts: `.planning/PROJECT.md`, `.planning/ROADMAP.md`, `.planning/STATE.md`, `.planning/intel/*.md`, `.planning/notes/*.md`, `.planning/seeds/*.md`, `.planning/research/*.md`, `.planning/todos/**.md`.
   - If `$ARGUMENTS` contains `--full`, also read `.planning/phases/**/*.md`.

2. **Extract these signals into the positioning brief**:
   - **Product name(s)** — site brand, codebase name, legacy names. Flag if there's drift.
   - **North-star one-liner** — the strategic line / tagline / memorable thing.
   - **Audiences (segments)** — every distinct ICP mentioned. Map each to its job-to-be-done if present.
   - **Value pillars** — the 5-10 things the product actually delivers.
   - **Advisory stance** — does the product take a position ("recommended", "best for…") or stay interpretive ("here are the facts, you decide")? Pull verbatim if stated.
   - **Banned phrases / verbs** — anything the brand explicitly refuses to say (e.g. "rekomenduojama", "verta", "comprehensive", "industry-leading").
   - **Shipped vs aspirational features** — what works TODAY vs what's marketed-ahead-of-product. This is the load-bearing input for the trust auditor.
   - **Honesty stance** — does the existing copy contain claims ahead of shipped capability? If so, list them.
   - **Pricing direction** — current prices, whether they're stale, whether B2B has hard prices or is "Susisiekime" only.
   - **Competitor landscape** — direct + indirect competitors mentioned in the repo.
   - **Geography / language** — primary market, secondary markets, UI language.
   - **Design system** — brand colors, typography, voice, the aesthetic name if one exists (e.g. "Calm Utility").

3. **For each audience segment, write a scaffold**:
   ```md
   # ICP: {segment}

   ## Job-to-be-done
   *(one sentence)*

   ## Pain points
   - *(from repo evidence)*

   ## Objections
   - *(from repo evidence; if none documented, mark "needs interview")*

   ## Real proof available
   - *(testimonials, pilots, data — or "none yet")*

   ## Primary CTA
   *(what action this segment should take)*

   ## Open questions
   - *(things the repo doesn't answer)*
   ```

4. **Write the positioning brief** as markdown to `.pmstack/positioning.md`. Use the structure listed above; cite the source file for every fact (`source: docs/PRD.md`, `source: DESIGN.md §Color`).

5. **Report a summary** to the user in chat (under 200 words):
   - Files read (count + paths).
   - Audiences found.
   - Brand-name drift (if any).
   - Top 3 honesty-stance risks (claims ahead of capability).
   - Anything else that surprised you.

6. **Detect sparse-context repos.** If the ingest produced a brief with any of:
   - Fewer than 3 documented audiences.
   - No documented advisory stance or banned-verb list.
   - Empty or `[needs-interview]` markers for ≥5 sections.
   - No DESIGN.md / brand voice docs at all.

   …then explicitly recommend `/pm:office-hours` in the summary: *"Your repo has limited marketing context. Run `/pm:office-hours` to fill the gaps via a 5-10 minute intake interview."*

   If the repo has NO marketing-adjacent MDs at all (greenfield), refuse to write `positioning.md` and tell the user to run `/pm:office-hours` instead — there's nothing to ingest.

## Hard rules

- Do not invent facts. Every claim in `positioning.md` must cite a source file.
- Do not edit any code files. Ingest is read-only outside `.pmstack/`.
- If you find conflicting decisions across MD files, list them in `.pmstack/positioning.md` under a "Conflicts" heading and surface them in the chat summary.
- If `.pmstack/` doesn't exist, create it. If `.pmstack/positioning.md` already exists, write a new version next to it as `.pmstack/positioning-{YYYY-MM-DD}.md` and let the user diff.
