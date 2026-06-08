# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of personal **Claude Code Skills** (productivity and finance). There is no application, build, test, or lint step — the deliverable is the skill content itself (Markdown), which Claude Code loads at runtime. "Correct" means a skill that triggers reliably and produces the intended output; validate by invoking the skill, not by running a test suite.

## Layout

Skills live under `skills/<category>/<skill-name>/`, each a self-contained directory:

```
skills/finance/stock-analysis/
├── SKILL.md                  # entry point: frontmatter + workflow
└── references/               # progressive-disclosure detail files
    ├── quantitative.md
    ├── qualitative.md
    └── output_format.md
```

## Skill authoring conventions

**`SKILL.md` is the contract.** It opens with YAML frontmatter:
- `name` — matches the directory name.
- `description` — this is what determines *when the skill fires*. It is written as a dense list of trigger phrasings and explicit "Do NOT use for…" exclusions, in the third person. When editing a skill's scope, edit the description with the same density — vague descriptions misfire.

**Progressive disclosure is the core pattern.** `SKILL.md` holds the high-level workflow as ordered steps and *points to* `references/*.md` for the heavy detail (scoring definitions, thresholds, exact output layout) rather than inlining it. The workflow says "Read `references/quantitative.md` before scoring"; the reference file owns the specifics. This keeps the decision logic and the presentation/format separable — e.g. the output template lives entirely in `references/output_format.md` so it can change without touching the analysis steps. Preserve this separation when extending a skill: logic in `SKILL.md`, lookup detail and formatting in `references/`.

**Cross-file consistency matters.** Symbol conventions, scorecard structure, and any thresholds are defined once (usually in a reference file) and referenced elsewhere. When changing one, grep the skill directory for the others so the rule stays singular.

## Note

`.DS_Store` files are gitignored but currently present on disk — ignore them.
