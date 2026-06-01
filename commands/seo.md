---
description: Produce a local-language SEO brief (keywords, schema, meta, content gaps) using the SEO / Local-search Lead subagent.
argument-hint: "[--lang lt|en|other]"
allowed-tools: Read, Glob, Grep, Write, WebSearch, Task
---

# /pm:seo

You are dispatching the SEO / Local-search Lead subagent.

## Procedure

1. **Determine target language**:
   - Default: read `lang` from `.pmstack/positioning.md` (e.g. `lang="lt"`).
   - Override: `--lang` flag.

2. **Determine geo + competitor list** from `.pmstack/positioning.md`. If competitors aren't documented, ask the user to name them before dispatching.

3. **Read current meta** (`app/layout.tsx`, `app/sitemap.ts`, `app/robots.ts`, `next-sitemap.config.js`, OG image components, schema.org JSON-LD).

4. **Dispatch the SEO / Local-search Lead subagent** (Task tool, `subagent_type: seo-local-search-lead`) with this brief:

   ```
   Produce an SEO brief for {site} targeting {geo} in {lang}.

   Competitors: {list}
   Current meta files: {paths}
   ICP segments documented: {list}

   Deliverables:

   ## Keyword universe
   Produce a table:
   | Query (in {lang}) | Intent | Volume tier | Difficulty tier | Why it matters | Suggested page |
   |---|---|---|---|---|---|

   Notes:
   - "Volume tier" = high/mid/low based on common sense in this geography; do not fabricate exact numbers.
   - "Difficulty tier" = competitor saturation, not exact KD.
   - 8-15 queries total. Mix branded, problem-based, intent ("kaip patikrinti…"), and commercial.

   ## Schema.org markup
   For each page type the site has (landing, pricing, FAQ, sample report, /explore):
   - Which schema type(s) apply (Product, FAQPage, SoftwareApplication, RealEstateListing, etc.)
   - Concrete JSON-LD scaffold the engineering team can paste in.

   ## Meta + OG tags
   For each landing page route documented:
   - title (≤60 chars)
   - description (≤155 chars)
   - OG image suggestion (size, content)
   - Twitter card type

   ## URL structure recommendations
   - Are current URLs clean / readable / localized? Flag anything that needs to change before launch (a URL change post-launch hurts more than it helps).

   ## Content gaps vs competitors
   - 3-5 pages the site needs that competitors have. Each with a brief justification.

   ## Local-search specifics ({geo})
   - Anything region-specific (hreflang, country-TLD, local-business schema, regional content).
   - For LT: include the LT diacritic rendering note (Newsreader/IBM Plex Mono support ū macron correctly; some serifs don't).

   Output to .pmstack/seo/{YYYY-MM-DD}.md.

   Hard rules:
   - Do not fabricate exact search volumes or KD scores. Tiers only.
   - WebSearch is available — use it to verify competitor URL structures and current SERPs in {geo}, but cite every search result in the brief.
   - Lithuanian queries must use Lithuanian diacritics correctly. No "patikrinkite" vs "patikrinkite" inconsistency.
   ```

5. **Report headline findings**: top 5 keywords by opportunity, 3 quickest meta fixes, biggest content gap.
