# pmstack

> Product-marketing stack for Claude Code. A gstack-shaped opinionated plugin that turns Claude Code into a virtual product-marketing team: positioning, conversion copy, trust audits, visual critique, LT/EU SEO, and A/B planning — built for product-led sites that need to look great and convert without making things up.

**Status:** v0.1 — initial release, tuned for [Relando](https://reportus-web.vercel.app/) (LT real-estate due diligence) but designed to generalize.

## Why pmstack exists

[gstack](https://github.com/garrytan/gstack) turns Claude Code into a virtual engineering team. pmstack is the marketing analog. Generic LLM marketing prompts hallucinate ICPs, invent stats, and write copy that sounds like every other SaaS landing page. pmstack instead:

1. **Reads your repo first.** Every subagent ingests your existing product/marketing MDs (PRDs, design systems, redesign plans, brand docs, TODO files) before saying anything.
2. **Refuses to fabricate.** A trust-and-objection auditor flags any claim ahead of shipped capability, any invented testimonial, any "comprehensive" / "best-in-class" / fake-stat phrasing.
3. **Knows the difference between B2C and B2B copy.** Audience subagent runs per segment; one product, multiple lenses.
4. **Outputs artifacts first, edits on approval.** Mirrors gstack's plan → build → ship loop. You stay in control.

## Quick start

```bash
# 1. Clone into your Claude Code plugins dir (or use the Claude Code plugin installer)
git clone https://github.com/drevinskas-darius/pmstack ~/.claude/plugins/pmstack

# 2. Open your marketing site repo in Claude Code
cd path/to/your/marketing-site

# 3. Run the ingest first — pmstack reads your MDs and builds an ICP/positioning brief
/pm:ingest

# 4. Then run any of the subagent commands
/pm:audience buyers     # ICP brief for a specific segment
/pm:copy hero           # rewrite a section per audience
/pm:trust-audit         # flag honesty / overpromise issues
/pm:visual-critique     # design heuristics + design-system compliance
/pm:seo                 # local-language SEO brief (LT default, English variants)
/pm:ab-plan hero        # variants + hypotheses for a section
/pm:handoff             # synthesize subagent output → diff plan
/pm:ship                # apply the approved diff to the site repo
```

## Commands

| Command | What it does | When to run |
|---------|-------------|-------------|
| `/pm:ingest` | Reads every `*.md` in the repo (PRD, DESIGN, REDESIGN-PLAN, TODOS, planning notes). Outputs a positioning brief + ICP scaffolds. | First. Then whenever the product context changes materially. |
| `/pm:audience <segment>` | Spawns the Audience Researcher subagent for one segment. ICP, JTBD, objections, primary CTA. | Before writing copy for a new audience. |
| `/pm:copy <section>` | Spawns Conversion Copywriter. Rewrites a section against AIDA/PAS/BAB, anchored to one audience. | When a section underperforms or is off-brand. |
| `/pm:trust-audit` | Spawns Trust & Objection Auditor. Flags claims ahead of shipped capability, fake stats, fabricated proof. | Before every launch. Mandatory CI step. |
| `/pm:visual-critique` | Spawns Visual Critic. Checks against your DESIGN.md + heuristics (hierarchy, density, motion). | After major visual changes. |
| `/pm:seo` | Spawns SEO / Local-search Lead. LT-default keyword + schema + meta + URL structure brief. | Quarterly, or before targeting a new geo/segment. |
| `/pm:ab-plan <section>` | Spawns A/B Test Planner. Variants ranked by expected lift + hypothesis + minimum sample size. | When traffic is high enough to test against. |
| `/pm:handoff` | Synthesizes the most recent subagent outputs into a single diff plan against your repo. | When you're ready to ship copy/visual changes. |
| `/pm:ship` | Applies the approved diff. Equivalent to gstack's `/ship`. | Last. Reviewed by you. |

## Subagents

Six opinionated subagents, each with a single job:

1. **Audience Researcher** (`agents/audience-researcher.md`) — segment-specific ICP, JTBD, objections. One report per audience.
2. **Conversion Copywriter** (`agents/conversion-copywriter.md`) — section-level rewrites against AIDA/PAS/BAB. Refuses to write outside your brand voice or banned-verb list.
3. **Trust & Objection Auditor** (`agents/trust-objection-auditor.md`) — the most important one. Flags any claim ahead of shipped capability, invented testimonials, refund guarantees, "comprehensive" / "best-in-class" / "industry-leading" phrasing, regulatory exposure.
4. **Visual Critic** (`agents/visual-critic.md`) — visual heuristics + your DESIGN.md compliance. Catches density issues, hierarchy violations, motion overuse, color contrast.
5. **SEO / Local-search Lead** (`agents/seo-local-search-lead.md`) — local-language SEO. Defaults to LT but documents how to adapt. Schema.org markup, meta, URL structure, content gaps vs competitors.
6. **A/B Test Planner** (`agents/ab-test-planner.md`) — variant scaffolds with explicit hypotheses + expected lift + minimum sample size. Doesn't propose A/B tests below traffic thresholds.

## Skills

Three skills extend pmstack's per-repo knowledge:

- `ingest-context` — how to read a marketing-adjacent repo (PRD, DESIGN, REDESIGN-PLAN, TODOS, planning artifacts) without missing anything.
- `relando-brand` — example skill: the Relando brand voice, tokens, banned verbs, advisory stance. Replace with your own brand skill or copy the structure.
- `icp-frameworks` — JTBD, PAS, AIDA, BAB, value-prop canvas. Concrete prompts the subagents pull from.

## Honesty stance (the load-bearing part)

pmstack's Trust & Objection Auditor enforces an **honest-now** stance by default. That means:

- ❌ No fabricated stats ("2,400+ reports", "98% satisfaction") unless they're in your repo with a source.
- ❌ No invented testimonials. Pro/B2B segments without real proof get **lead-capture CTAs** ("Susisiekime"), not fake social proof.
- ❌ No "comprehensive" / "complete" / "all-in-one" if the product doesn't actually deliver that today.
- ❌ No refund / SLA / guarantee claims unless you have the policy committed.
- ✅ Marketing matches what the product delivers today. Future capabilities are marked as roadmap, not present tense.

This is overridable per-command (`--full-vision`) but the default is honest-now. Marketing copy that survives an audit also survives EU consumer-protection law (UCPD 2005/29/EC, equivalent regimes elsewhere).

## How it composes

```
/pm:ingest
   ↓ produces  .pmstack/positioning.md  +  .pmstack/icp/{segment}.md
/pm:audience buyers / brokers / developers
   ↓ produces  .pmstack/icp/{segment}.md  (refined)
/pm:copy hero / value-props / pricing / faq / cta
   ↓ produces  .pmstack/copy/{section}-{segment}.md  (multiple variants)
/pm:visual-critique
   ↓ produces  .pmstack/critique/{date}.md
/pm:trust-audit
   ↓ produces  .pmstack/audits/{date}.md   ← BLOCKS /pm:handoff if it finds issues
/pm:seo
   ↓ produces  .pmstack/seo/{date}.md
/pm:ab-plan hero
   ↓ produces  .pmstack/ab/{section}-{date}.md
/pm:handoff
   ↓ produces  .pmstack/diff/{date}.patch   ← reviewable diff against your repo
/pm:ship
   ↓ applies the patch (after your review)
```

## Compatibility

pmstack is a **Claude Code plugin**. It works in:

- Claude Code (CLI) — the primary target.
- Claude Code in the Anthropic Console.
- Any Claude Agent SDK setup that supports the plugin contract (commands, agents, skills).

It's framework-agnostic for the underlying site — Next.js, SvelteKit, Astro, Remix, plain HTML all work. The visual-critique and copy subagents detect the framework and adjust their edit format.

## Public roadmap

- v0.1 — initial release with six subagents + handoff + ship loops (this commit).
- v0.2 — `/pm:icp-interview` — generate interview scripts for un-validated segments; record findings back into ICP files.
- v0.3 — `/pm:competitive-brief` — competitor scrape + positioning gap analysis. Integrates with the existing `competitive-brief` plugin where present.
- v0.4 — `/pm:growth-loop` — diagram the acquisition → activation → retention loop and identify the highest-leverage gap.
- v1.0 — multi-language support + per-region brand skills + opinionated CRO playbook.

## Contributing

Open a PR. Per-segment brand skills are the most useful contribution — drop a `skills/{brand-name}/` directory with a `SKILL.md` and the subagents will route to it when the repo matches.

## License

MIT. See `LICENSE`.

## Acknowledgements

- [gstack](https://github.com/garrytan/gstack) — the shape and naming convention.
- [Anthropic Skills](https://github.com/anthropics/skills) — `competitive-brief`, `synthesize-research`, and the cowork plugin system.
- [Corey Haines' marketingskills](https://github.com/coreyhaines31/marketingskills) — proof that marketing-as-skill-pack works.
