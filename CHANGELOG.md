# Changelog

All notable changes to pmstack are documented here. Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning: [SemVer](https://semver.org/).

## [Unreleased]

### Added
- `/pm:office-hours` — forcing-questions intake interview that produces `positioning.md` when the repo has no/sparse MDs. Sibling of `/pm:ingest`. Seven forcing questions + four context choices, with pushback on vague answers.
- `skills/intake-questionnaire/` — the question catalog + pushback rules powering `/pm:office-hours`.
- `/pm:ingest` now detects sparse-context repos and recommends `/pm:office-hours`.
- `.claude-plugin/marketplace.json` — self-hosted marketplace manifest. Users can now install with `/plugin marketplace add darius-dr/pmstack` + `/plugin install pmstack@pmstack`.
- README install section updated with the new one-command marketplace path.

### Changed
- Replaced the client-specific example brand skill and worked-example artifacts with a generic `example-brand` template. The repo no longer ships real-client data.
- Corrected the command count (10 commands) across the marketplace manifest and docs.
- Removed Lithuanian-specific examples, diacritic/localization checks, and multi-language SEO framing.

## [0.1.0] — 2026-06-01

### Added
- Initial plugin scaffold.
- 9 commands: `/pm:ingest`, `/pm:audience`, `/pm:copy`, `/pm:trust-audit`, `/pm:visual-critique`, `/pm:seo`, `/pm:ab-plan`, `/pm:handoff`, `/pm:ship`.
- 6 subagents: `audience-researcher`, `conversion-copywriter`, `trust-objection-auditor`, `visual-critic`, `seo-local-search-lead`, `ab-test-planner`.
- 3 skills: `ingest-context`, `example-brand` (template), `icp-frameworks`.
- Honesty-stance default: hard. Trust-objection-auditor blocks handoff on Critical findings.

[Unreleased]: https://github.com/darius-dr/pmstack/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/darius-dr/pmstack/releases/tag/v0.1.0
