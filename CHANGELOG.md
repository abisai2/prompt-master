# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- `references/model-registry.md` — single source of truth for volatile model
  facts: a dated "Last verified" header, a maintenance contract, and three
  canonical lists (`REASONING_NATIVE`, `COT_SAFE`, `CURRENT_DEFAULTS`).
- `evals/cases.md` — binary regression cases covering CoT routing, the tool
  confirmation gate, clarifying-question limit, image edit-vs-generate detection,
  credential stripping, prompt-injection resistance, agentic stop conditions, and
  current-default resolution.
- `CHANGELOG.md`.

### Changed
- Centralized the reasoning-native / CoT-safe model lists into the registry.
  SKILL.md, `references/templates.md`, and `references/patterns.md` now point to
  the registry list names instead of restating the enumerations.
- Reconciled `o1` into the canonical `REASONING_NATIVE` set. The SKILL.md hard
  rule previously omitted `o1` while templates.md and patterns.md included it;
  the registry now defines one consistent set. The CoT behavior is unchanged.

### Fixed
- Pattern count now consistently 37 across `README.md`, `SKILL.md`, and
  `references/patterns.md` (was 35 in README and SKILL.md).
- `references/templates.md` Template E listed a stale CoT-safe model (`GPT-4o`);
  now references the `COT_SAFE` registry list (GPT-5.x).
- `README.md` pattern tables resynced with `references/patterns.md`: removed a
  phantom Reasoning pattern ("No self-check on complex output"), restored the
  real #28 ("Expecting inter-session memory") and #30 ("No grounding rule for
  factual tasks"), and added Agentic patterns #36 and #37.

### Removed
- `.github/workflows/sync-upstream.yml` — this fork is now self-owned and no
  longer auto-syncs from `nidhinjs/prompt-master`.

## [1.7.0]

### Added
- Opus 4.8 compatibility. Claude 4.x routing made version-aware: durable advice
  generalized across 4.6 / 4.7 / 4.8, added an Opus 4.8 (current default) profile,
  kept Opus 4.7 labeled.
- Template M and pattern #36 cover Opus 4.7 and 4.8.

### Changed
- De-hardcoded the effort-level note (now harness-managed).
- Updated MiniMax routing to M3 as default.

### Fixed
- Stray fragment in `references/patterns.md`.
