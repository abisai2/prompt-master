# Updating This Skill

How to keep `prompt-master` current as the LLM landscape changes. The skill is
structured so most updates touch exactly one file.

## 1. The registry is the single lever

For ~90% of changes, edit only [`references/model-registry.md`](references/model-registry.md):
the three canonical lists plus the `Last verified` date. `SKILL.md`,
`references/templates.md`, and `references/patterns.md` all point there — never
restate model lists in those files.

| What changed | Where it goes |
|--------------|---------------|
| New model that reasons internally (o-series, R1, thinking modes) | `REASONING_NATIVE` |
| New standard model where Chain of Thought helps | `COT_SAFE` |
| A provider's flagship shifts (e.g. Opus 4.9, GPT-6, Gemini 4) | `CURRENT_DEFAULTS` |
| A model moves between thinking / non-thinking | move it between the two lists |
| A brand-new **tool** (not a model) | a per-tool routing section in `SKILL.md` → Tool Routing (separate from the registry) |

Always bump `Last verified` even if nothing changed — that date is the staleness signal.

## 2. Cadence

- Review monthly, **plus** on any major model launch (the release is the trigger;
  the calendar is the backstop).
- Run [`evals/cases.md`](evals/cases.md) after every edit. The stale-name canary
  (case #4) and the CoT cases catch the most common regressions — paste the cases
  at Claude and have it self-check.
- Log every change under `CHANGELOG.md` → `[Unreleased]`. Bump the version in
  `SKILL.md` frontmatter when you cut a release.

## 3. Harvesting upstream

This fork is self-owned (no auto-sync), but the original author still ships.
Pull changes deliberately instead of blind fast-forward:

```bash
git fetch upstream
git log --oneline main..upstream/main         # what's new upstream
git diff main...upstream/main -- SKILL.md      # inspect before taking anything
```

Then cherry-pick or merge what you want on a branch and open a PR. Your fork's
changes stay; you adopt upstream's deliberately.

The `upstream` remote points to `https://github.com/nidhinjs/prompt-master.git`.
If it is missing on a fresh clone, add it:

```bash
git remote add upstream https://github.com/nidhinjs/prompt-master.git
```

## 4. Release checklist

1. Registry lists + `Last verified` date updated.
2. `evals/cases.md` pass (no regressions; canary clean).
3. `CHANGELOG.md` `[Unreleased]` entries written.
4. Version bumped in `SKILL.md` frontmatter and a new `CHANGELOG.md` section cut.
