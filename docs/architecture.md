# pmstack architecture

A 5-minute read for contributors.

## Mental model

pmstack = **gstack for marketing**.

gstack turns Claude Code into a virtual engineering team by giving it 28 slash commands that activate distinct cognitive modes (CEO, eng manager, designer, reviewer, QA, security, release engineer). pmstack does the same for product marketing: 8 commands that route to 6 opinionated subagents, each with a single job.

The shape is identical. The opinions are different.

## The flow

```
                        ┌──────────────────────┐
                        │   /pm:ingest         │
                        │   (read repo MDs)    │
                        └──────────┬───────────┘
                                   │
                ┌──────────────────┼──────────────────┐
                ▼                  ▼                  ▼
        ┌────────────┐     ┌────────────┐     ┌────────────┐
        │/pm:audience│     │/pm:copy    │     │/pm:visual- │
        │            │     │            │     │critique    │
        └─────┬──────┘     └─────┬──────┘     └─────┬──────┘
              │                  │                  │
              ▼                  ▼                  ▼
       audience-researcher   conversion-          visual-critic
       (writes ICP brief)    copywriter           (writes critique)
                             (writes variants)

                ┌──────────────────┬──────────────────┐
                ▼                  ▼                  ▼
        ┌────────────┐     ┌────────────┐     ┌────────────┐
        │/pm:seo     │     │/pm:ab-plan │     │/pm:trust-  │
        │            │     │            │     │audit       │
        └─────┬──────┘     └─────┬──────┘     └─────┬──────┘
              │                  │                  │
              ▼                  ▼                  ▼
        seo-local-search-     ab-test-planner    trust-objection-
        lead                  (writes plan)      auditor
        (writes brief)                           (writes audit)
                                                       │
                                                       │ blocks if
                                                       │ critical>0
                                                       ▼
                                              ┌────────────────┐
                                              │ /pm:handoff    │
                                              │ (synthesize    │
                                              │  → diff plan)  │
                                              └───────┬────────┘
                                                      │
                                                      ▼
                                              ┌────────────────┐
                                              │ /pm:ship       │
                                              │ (apply diff,   │
                                              │  user reviews) │
                                              └────────────────┘
```

## Why subagents + commands?

**Commands** are the user-facing entry points. Each one is a single concern (audience, copy, visual, etc.). Easy to remember, easy to chain.

**Subagents** carry the opinions. Each subagent has:
- A name + description.
- A single job.
- A hard-rules list.
- An output contract (the exact file shape it produces).
- An anti-pattern list (things it refuses to do).

Splitting commands from subagents lets you:
- Add a new command that reuses an existing subagent (e.g. `/pm:copy-rewrite-all` could fan out to the same `conversion-copywriter` for every section).
- Add a new subagent without inventing a new command surface (e.g. `legal-review` could be invoked by `/pm:trust-audit` for complex regulatory scopes).

## The honesty stance

pmstack's load-bearing opinion: **default to honest-now**.

- The Trust & Objection Auditor blocks handoff if it finds Critical issues.
- The Conversion Copywriter refuses to write variants that need fabricated proof.
- The Audience Researcher refuses to invent demographics or testimonials.
- The A/B Test Planner refuses to scaffold tests below traffic thresholds.

Override available: `--full-vision` on any command. The plugin will surface the override in audit logs.

## File structure

```
pmstack/
├── .claude-plugin/
│   └── plugin.json           # manifest
├── commands/                 # slash commands (user-facing)
│   ├── ingest.md
│   ├── audience.md
│   ├── copy.md
│   ├── trust-audit.md
│   ├── visual-critique.md
│   ├── seo.md
│   ├── ab-plan.md
│   ├── handoff.md
│   └── ship.md
├── agents/                   # subagents (carry opinions)
│   ├── audience-researcher.md
│   ├── conversion-copywriter.md
│   ├── trust-objection-auditor.md
│   ├── visual-critic.md
│   ├── seo-local-search-lead.md
│   └── ab-test-planner.md
├── skills/                   # composable knowledge
│   ├── ingest-context/SKILL.md
│   ├── relando-brand/SKILL.md     # example brand skill
│   └── icp-frameworks/SKILL.md
├── docs/
│   └── architecture.md       # this file
├── README.md
├── LICENSE
└── .gitignore
```

## Output structure (created in the target repo)

```
.pmstack/
├── positioning.md            # single source of truth (from /pm:ingest)
├── icp/
│   ├── buyers.md
│   ├── brokers.md
│   └── developers.md
├── copy/
│   ├── hero-buyers.md
│   ├── hero-brokers.md
│   ├── pricing-buyers.md
│   └── ...
├── critique/
│   └── 2026-06-15-1430.md
├── audits/
│   └── 2026-06-15-1500.md
├── seo/
│   └── 2026-06-15.md
├── ab/
│   └── hero-2026-06-15.md
└── diff/
    └── 2026-06-15-1530-plan.md
```

The `.pmstack/` directory is committed to the repo so the team can review the artifacts. Only `.pmstack/cache/` is gitignored.

## Adding a brand skill for your project

The `skills/relando-brand/SKILL.md` file is an example. To add your own brand:

1. Create `skills/{your-brand}/SKILL.md`.
2. Follow the structure of the Relando file (Identity → Aesthetic → Typography → Colors → Voice → Audiences → Shipped/Not-shipped → Legal constraints).
3. Reference it from your repo's `.pmstack/positioning.md` so the subagents route to it.

Brand skills are the highest-leverage contribution — pmstack subagents are only as sharp as the brand voice they're working with.

## Versioning

- `0.x` — pre-stable. Breaking changes to file layouts allowed; expect to migrate `.pmstack/` artifacts manually.
- `1.0` — stable file layouts + command surface. Subagent opinions can iterate, file structures cannot.

## Comparison with gstack

| Concern | gstack | pmstack |
|---|---|---|
| Domain | Engineering | Product marketing |
| Subagents | 23 (CEO, eng manager, designer, …) | 6 (audience, copy, trust, visual, SEO, A/B) |
| Output | PR / commit | `.pmstack/` artifacts + a diff plan |
| Gate | Codex quality gate before file | Trust audit blocks handoff |
| Browser | Persistent headless Chromium | None (file-level work) |
| Stack ownership | Full eng workflow | Marketing artifacts; you commit code |

## Comparison with `marketingskills` (Corey Haines)

| Concern | marketingskills | pmstack |
|---|---|---|
| Form | Skill pack | Plugin (commands + agents + skills) |
| Opinions | Per-skill | Per-subagent, with hard rules |
| Honesty default | Soft | Hard (auditor blocks handoff) |
| Output | Per-skill | Structured artifact tree (`.pmstack/`) |
| Audience model | General | Per-segment ICP files |
| Best for | One-off tasks | Iterative marketing cycle |

Both work alongside each other. pmstack focuses on positioning, audience fit, conversion copy, trust audits. marketingskills covers more growth-engineering ground (analytics tracking, SEO technical, paid funnels). Use both.

## Contributing

PRs welcome. The highest-leverage contributions:
- Per-brand skills (drop a `skills/{brand}/SKILL.md`).
- Per-vertical ICP frameworks (e.g. fintech, healthtech, marketplaces).
- Trust-audit checklists for specific regulatory regimes (GDPR-EU, CCPA, FTC, sectoral).
- Localization skills (LT today; PL/EE/LV/DE are the obvious next).
