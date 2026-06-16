---
description: Rewrite a landing-page section for one or more audiences using the Conversion Copywriter subagent.
argument-hint: "<section> [--segment <name>] [--framework AIDA|PAS|BAB]"
allowed-tools: Read, Glob, Grep, Write, Task
---

# /pm:copy

You are dispatching the Conversion Copywriter subagent for the section named in `$ARGUMENTS`.

## Procedure

1. **Parse arguments**:
   - First positional: section name (`hero`, `value-props`, `pricing`, `testimonials`, `faq`, `cta`, `audience-band`, etc.).
   - `--segment {name}`: which audience this variant targets (default: all segments documented in `.pmstack/icp/`).
   - `--framework {AIDA|PAS|BAB}`: copy framework (default: choose per section — Hero=PAS, Value-props=BAB, Pricing=AIDA).

2. **Verify prerequisites**:
   - `.pmstack/positioning.md` must exist (else: tell user to run `/pm:ingest`).
   - `.pmstack/icp/{segment}.md` must exist for the requested segment (else: tell user to run `/pm:audience {segment}`).

3. **Locate the current section in the repo**. Use Glob + Grep to find the component file(s) that render this section. Common patterns:
   - Next.js: `components/{section}.tsx`, `components/{section}-section.tsx`, `app/(marketing)/page.tsx`.
   - SvelteKit / Astro: similar component naming.
   Read the current copy verbatim so the rewrite has a baseline to beat.

4. **Dispatch the Conversion Copywriter subagent** (Task tool, `subagent_type: conversion-copywriter`) with this brief:

   ```
   Rewrite the {section} section for the {segment} audience.

   Framework: {framework}
   Current copy (verbatim): {paste current section text}
   ICP brief: .pmstack/icp/{segment}.md
   Positioning: .pmstack/positioning.md

   Output 3 variants to .pmstack/copy/{section}-{segment}.md. For each variant:
   - Headline (≤8 words)
   - Sub (≤20 words)
   - Body (3 sentences max)
   - CTA label (2-4 words)
   - The single best reason this variant should beat the current copy

   Then add a "Recommended" section that picks one variant and explains why.

   Hard rules:
   - Never use the brand's banned-verb list (read it from positioning.md).
   - Never invent stats, testimonials, or proof. If the variant needs proof to land, write "[proof: {what you need}]" and stop.
   - Stay inside the advisory stance documented in positioning.md (interpretive vs recommendatory).
   ```

5. **Report a summary** to the user: which framework was used, the recommended variant's headline, and what proof (if any) is needed for the variant to ship.
