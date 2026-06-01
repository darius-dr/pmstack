---
description: Critique the marketing site visually against the project's DESIGN.md + general heuristics.
argument-hint: "[section] (optional, critique only that section)"
allowed-tools: Read, Glob, Grep, Write, Task
---

# /pm:visual-critique

You are dispatching the Visual Critic subagent.

## Procedure

1. **Read DESIGN.md** (or `DESIGN_SYSTEM.md`, `BRAND.md`, whichever the repo uses). If none exists, fall back to general visual heuristics + note this gap in the critique header.

2. **Find component + style files** relevant to the scope. If `$ARGUMENTS` is a section, scope to that section's component(s); otherwise audit the whole landing page (`app/page.tsx` + every component it imports).

3. **Dispatch the Visual Critic subagent** (Task tool, `subagent_type: visual-critic`) with this brief:

   ```
   Critique the visual implementation of {section or "the landing page"} against {DESIGN.md path or "general visual heuristics"}.

   Files to read:
   {list of files}

   Heuristics to apply (each is a check, NOT a generic remark):

   DESIGN-SYSTEM COMPLIANCE:
   - Are colors only from the documented token set? Flag hex-codes not in DESIGN.md.
   - Are font families restricted to the documented set? Flag stray font-family declarations.
   - Are radius values, spacing values, shadows only from the documented scale?
   - Is the aesthetic-name's signature device (e.g. "uncover/reveal" motif, "hairline" rules, "mono-for-data") actually present? Where is it missing?

   HIERARCHY + DENSITY:
   - Does the eye know where to land first on each section? Identify the visual anchor.
   - Is any section too dense (>6 elements competing for attention)?
   - Is any section too sparse (<3 elements, looking unfinished)?
   - Are headings sized to actually feel like headings, or do they read as body text?

   CONVERSION-CRITICAL ELEMENTS:
   - CTAs: prominent, repeated at expected scroll depths, single primary color, scannable verbs.
   - Forms: minimum-viable fields, error states visible without JS.
   - Trust signals: positioned near friction points (purchase, email-capture), not buried in the footer.

   MOTION:
   - Is motion intentional or decorative? Flag anything that animates "because it can".
   - Is reduced-motion respected? grep for `prefers-reduced-motion`.

   ACCESSIBILITY:
   - Color contrast on every text/bg pair (sample 5-10 critical pairs and check WCAG AA).
   - Focus styles present on interactive elements?
   - Tap targets ≥44px on mobile-likely components (buttons, segmented controls, links).

   LOCALIZATION:
   - If lang=lt or any non-ASCII language: do the chosen fonts render diacritics correctly? (Common LT trap: certain serifs mis-position ū macron.)

   Output to .pmstack/critique/{YYYY-MM-DD}-{HHMM}.md with structure:

   # Visual Critique — {date}

   ## Strongest moments
   - 3-5 things the site does well. Be specific (component:line if relevant).

   ## Critical issues (block ship)
   - Each with: location, what's wrong, suggested fix.

   ## High issues (must fix before launch)
   - Same format.

   ## Medium issues (worth fixing)
   - Same format.

   ## Low / polish
   - One line each.

   ## Specific suggestions to make the site "look great"
   - 5-10 concrete moves that would raise the visual ceiling. Each must reference a specific component or section.

   Hard rules:
   - No generic remarks ("could use more whitespace"). Every finding cites a file:line or section:element.
   - Don't propose redesigns; propose adjustments within the documented system.
   - If you'd genuinely recommend going outside the documented system, mark it "Brand-stretch proposal" and explain the trade-off.
   ```

4. **Report headline counts** to the user + the 3 most impactful suggestions.
