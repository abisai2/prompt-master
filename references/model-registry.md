# Model Registry

Single source of truth for volatile model facts. Every model name, reasoning-mode
classification, and current-default referenced by the skill's Chain-of-Thought
rule lives here and nowhere else. SKILL.md, templates.md, and patterns.md point to
the canonical lists below by name — they never restate them.

**Last verified:** 2026-06-21

---

## Maintenance contract

When the model landscape changes:

1. Edit only the three canonical lists below and the **Last verified** date.
2. Do not restate these lists in SKILL.md, templates.md, or patterns.md — those
   files reference the list names (`REASONING_NATIVE`, `COT_SAFE`,
   `CURRENT_DEFAULTS`). Add new model names only here.
3. Per-tool routing sections in SKILL.md keep their own model names (each tool
   documents itself). They are not part of these lists — leave them as-is unless
   the tool's own behavior changed.
4. If a model moves between `REASONING_NATIVE` and `COT_SAFE`, move it in both
   lists in this file — the skill files need no edit.

---

## Canonical lists

These three lists are the only place these enumerations are spelled out.

**REASONING_NATIVE** — reasoning-native models. They think internally; adding
Chain of Thought, "think step by step", or reasoning scaffolding degrades output.
Never apply CoT to these.

- o1
- o3
- o4-mini
- DeepSeek-R1
- Qwen3 (thinking mode)

**COT_SAFE** — standard reasoning models. Chain of Thought helps on logic, math,
and debugging tasks.

- Claude (standard / non-thinking)
- GPT-5.x
- Gemini
- Qwen2.5
- Llama
- Mistral

**CURRENT_DEFAULTS** — the current default model to assume when a provider is named
without a specific version.

- Claude → Opus 4.8
- OpenAI → GPT-5.x / o3
- Gemini → Gemini 3 Pro

---

## Provider quick reference

This table is a convenience view only. The three lists above are authoritative.

| Provider | Current default | Reasoning-native variants | Notes |
|----------|-----------------|---------------------------|-------|
| Anthropic | Opus 4.8 | extended thinking mode | Standard Claude is COT_SAFE; thinking mode reasons internally |
| OpenAI | GPT-5.x / o3 | o1, o3, o4-mini | GPT-5.x is COT_SAFE; o-series is REASONING_NATIVE |
| Google | Gemini 3 Pro | — | Gemini is COT_SAFE |
| DeepSeek | — | DeepSeek-R1 | R1 outputs reasoning in `<think>` tags |
| Qwen | — | Qwen3 (thinking) | Qwen2.5 is COT_SAFE; Qwen3 has thinking + non-thinking modes |
| Meta / Mistral | — | — | Llama and Mistral are COT_SAFE |
