# Contributing to pmstack

Thanks for considering a contribution. pmstack is opinionated by design — most PRs should sharpen existing opinions, add brand skills, or extend region/vertical coverage. Brand-new commands or subagents are rare and need design review first.

## Highest-leverage contributions

1. **Per-brand skills** — drop `skills/{brand}/SKILL.md` in the structure of `skills/relando-brand/SKILL.md`. This is where pmstack gets sharp.
2. **Per-vertical ICP frameworks** — fintech, healthtech, marketplaces, dev tools, etc.
3. **Regulatory trust-audit checklists** — sectoral compliance regimes the auditor can apply (GDPR-EU consumer protection, HIPAA marketing rules, FTC truth-in-advertising, FCA financial promotions).
4. **Localization** — pmstack defaults to Lithuanian-aware tone + diacritic handling. PL/EE/LV/DE/SE are the obvious next.

## Design principles (non-negotiable)

1. **Honesty default is hard.** A subagent that softens the honesty stance loses its job.
2. **Cite or strike.** Every assertion in a generated artifact must point to a source file or be flagged `[needs verification]`. No exceptions.
3. **One job per subagent.** A subagent that does two things does both badly.
4. **Refuse, don't approximate.** When the data isn't there, subagents refuse and ask for it — they don't make up a plausible answer.
5. **Output a single artifact per run.** Never produce 4 files when 1 will do.

## Pull request process

1. Open an issue first if you're proposing a new command or subagent.
2. For skill additions / opinion sharpening, PR directly.
3. Run the example flows in `examples/` to make sure no contract changed.
4. Update `CHANGELOG.md` in the `[Unreleased]` section.
5. Update `README.md` if user-facing behavior changes.
6. Keep PR descriptions short. List what changed and why — not how.

## What pmstack will NOT accept

- Subagents that recommend dark patterns (urgency timers without basis, fake scarcity, etc.).
- Trust-audit relaxations to make stakeholders happy.
- Generic "AI-powered marketing automation" features (pmstack is opinionated artisanship, not a SaaS platform).
- Vendor-specific integrations as core commands (Mailchimp, HubSpot, etc. — these belong in separate plugins).
- Copy frameworks that lean on emotional manipulation as their primary lever.

## License

By contributing you agree your contributions are MIT-licensed under this repo.
