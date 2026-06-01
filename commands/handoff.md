---
description: Synthesize the most recent pmstack outputs into a single reviewable diff plan against the site repo.
argument-hint: "[--since <date>] [--include audience,copy,visual,seo]"
allowed-tools: Read, Glob, Grep, Write
---

# /pm:handoff

You are the synthesis step. Collect the freshest pmstack artifacts and produce one diff plan the user can review and then `/pm:ship`.

## Procedure

1. **Check for a blocking audit**. Read `.pmstack/audits/` for the most recent file. If its summary line says "Block /pm:handoff: yes", refuse to run and tell the user to address the Critical findings first. List them.

2. **Collect the freshest artifacts**:
   - `.pmstack/positioning.md` (the source of truth).
   - Latest ICP file per segment: `.pmstack/icp/{segment}.md`.
   - Latest copy variants: `.pmstack/copy/**.md` modified since the last handoff.
   - Latest visual critique: `.pmstack/critique/{date}.md` (top by date).
   - Latest SEO brief: `.pmstack/seo/{date}.md`.
   - Latest A/B plans: `.pmstack/ab/**.md` (if any).

3. **Produce the diff plan** at `.pmstack/diff/{YYYY-MM-DD}-{HHMM}-plan.md`:

   ```md
   # Handoff Plan — {date}

   ## Scope of this handoff
   - Audiences refined: {list}
   - Sections rewritten: {list}
   - Visual issues addressed: {count}
   - SEO changes: {count}

   ## File-by-file diff plan

   For each file the handoff will touch:

   ### {path/to/file.tsx}
   - **Lines:** {line range}
   - **Change type:** copy | layout | meta | tokens
   - **Before:** ```{snippet}```
   - **After:** ```{snippet}```
   - **Why:** {one sentence, citing the artifact}
   - **Risk:** {what could go wrong + how to verify post-ship}

   ## Pages or sections this handoff intentionally does NOT touch
   - {list with reasons — usually "needs proof we don't have"}

   ## Pre-ship checklist (manual)
   - [ ] Trust audit re-run after final diff applied: 0 Critical.
   - [ ] Visual diff (Chromatic / Percy / manual) screenshots reviewed.
   - [ ] Lighthouse run on /, /pricing, /precheck (current baseline + new).
   - [ ] LT diacritic spot-check on hero / pricing / footer.
   - [ ] Stripe price IDs unchanged (or intentionally changed with billing team).

   ## Suggested commit message
   ```
   marketing: {section list} rewrite for {segment list} (pmstack {date})

   - {one bullet per significant change}
   - Trust audit: clean
   - Visual critique: {N} addressed, {M} deferred (see .pmstack/critique/…)
   ```

   ## Next commands
   - `/pm:ship` to apply this plan.
   - `/pm:trust-audit` to re-run the audit on the proposed changes.
   ```

4. **Report a summary** to the user: # of files touched, # of intentional no-touches, link to the plan file.

## Hard rules

- Do not edit code files yourself. This step is plan-only.
- If you find that a planned change has no supporting artifact (no ICP, no copy variant, no audit finding), exclude it from the plan and surface it as "Drift detected — please run /pm:copy {section} first".
- The plan must be readable by a non-pmstack reviewer (e.g. the founder, an engineer) without explanation.
