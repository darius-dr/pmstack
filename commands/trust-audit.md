---
description: Audit the marketing site for honesty / overpromise / regulatory exposure. Output blocks /pm:handoff if it finds critical issues.
argument-hint: "[section] (optional, audit only that section)"
allowed-tools: Read, Glob, Grep, Write, Task
---

# /pm:trust-audit

You are dispatching the Trust & Objection Auditor subagent. This is the most important command in pmstack — it's the gate that prevents shipping copy that's legally or ethically exposed.

## Procedure

1. **Verify prerequisites**: `.pmstack/positioning.md` exists. If not, run `/pm:ingest` first.

2. **Find every user-facing string in the repo**. Default scope: the entire site repo. If `$ARGUMENTS` is non-empty, scope to that section only.
   - Component files: `components/**.tsx`, `app/**.tsx`, `app/**/page.tsx`, `lib/data.ts` (or equivalent copy file).
   - Static content: `public/**.md` if present.
   - Meta: `app/layout.tsx`, `app/sitemap.ts`, `app/robots.ts`, OG image tags.
   - Newest copy variants in `.pmstack/copy/**.md`.

3. **Dispatch the Trust & Objection Auditor subagent** (Task tool, `subagent_type: trust-objection-auditor`) with this brief:

   ```
   Audit the user-facing copy against the honesty stance documented in .pmstack/positioning.md.

   Read these files and scan for the listed risks:
   {list of files}

   Risks to flag (severity-ranked):

   CRITICAL (blocks /pm:handoff):
   - Claims of capability ahead of shipped product (e.g. "comprehensive due diligence" when feature X isn't built).
   - Invented testimonials, stats, or partner names.
   - Refund / SLA / guarantee claims not backed by a committed policy.
   - Regulatory exposure: language that risks violating consumer-protection law (UCPD 2005/29/EC, FTC truth-in-advertising, etc.). Flag with the specific clause if you can.
   - Banned-verb violations (read banned list from positioning.md).

   HIGH (must be addressed before launch):
   - Vague superlatives ("best", "leading", "#1", "industry-leading") without proof.
   - Borrowed-credibility traps (logos of partners that aren't real partners).
   - Advisory-stance violations (recommendatory phrasing in interpretive products, or vice versa).
   - Stale facts (prices, dates, feature lists out of sync with product).

   MEDIUM (worth fixing, won't block):
   - Inconsistent voice / tone between sections.
   - Section-to-section contradictions in positioning.

   LOW (note for follow-up):
   - Clarity / readability issues.
   - Accessibility issues in copy (jargon, sentence length).

   Output to .pmstack/audits/{YYYY-MM-DD}-{HHMM}.md with the structure:

   # Trust Audit — {date}

   ## Summary
   - Critical: N · High: N · Medium: N · Low: N
   - Block /pm:handoff: yes|no (yes if Critical > 0)

   ## Findings
   For each finding:
   ### [SEVERITY] {short title}
   - **File:line:** {path}:{line}
   - **Quote:** "…"
   - **Risk:** {what's wrong, in one sentence}
   - **Regulatory cite:** {if applicable}
   - **Fix:** {concrete rewrite or "remove"}

   ## Pass-list
   Things you checked that passed (one line each, max 20). Builds reviewer confidence.

   Hard rules:
   - Cite verbatim quotes; never paraphrase a flagged claim.
   - If unsure whether a claim is true or false, mark it UNKNOWN with a "needs verification" note — do NOT mark it Critical without evidence.
   - Be specific. "Vague" is not a finding; "Vague superlative on line 42 with no proof source" is.
   ```

4. **Report the audit headline** to the user: counts by severity, whether `/pm:handoff` is blocked, and the top 3 Critical findings (if any).
