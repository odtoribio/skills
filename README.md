# skills

A collection of personal custom [Agent Skills](https://agentskills.io) for productivity and finance.

Each skill is a self-contained folder with a `SKILL.md` (and optional `references/`). Drop that folder into Claude and it loads automatically, activating when your request matches what the skill is for.

## Available skills

| Skill | What it does |
|-------|--------------|
| [`stock-analysis`](skills/finance/stock-analysis) | Runs a full fundamental analysis on a stock (16 quantitative + 10 qualitative criteria) and delivers a clear **Yes / Intermediate / No** buy verdict. |

## Installing a skill

The examples below use **`stock-analysis`**. Substitute the path of any other skill the same way — the folder you install is always the one that contains `SKILL.md` (e.g. `skills/finance/stock-analysis/`).

First, get the files:

```bash
git clone https://github.com/odtoribio/skills.git
cd skills
```

### Claude Code (CLI / IDE)

Copy the skill folder into your skills directory:

```bash
# Personal — available in all your projects
mkdir -p ~/.claude/skills
cp -R skills/finance/stock-analysis ~/.claude/skills/

# …or Project — only this repo, commit it with the project
mkdir -p .claude/skills
cp -R skills/finance/stock-analysis .claude/skills/
```

You should end up with `~/.claude/skills/stock-analysis/SKILL.md`. Then:

- If `~/.claude/skills/` already existed, the new skill is picked up **in the current session** — no restart.
- If you just created `~/.claude/skills/` for the first time, **restart Claude Code** so it starts watching the directory.

Use it by asking naturally ("is NVDA a good buy?") or by invoking it directly with `/stock-analysis`.

### Claude web & desktop app

Custom skills are uploaded as a **ZIP of the skill folder** (Free, Pro, Max, Team, and Enterprise plans).

1. **Enable code execution first** — skills won't run without it.
   - Free / Pro / Max: **Settings → Capabilities →** turn on *Code execution and file creation*.
   - Team / Enterprise: an org owner enables *Code execution and file creation* **and** *Skills* under **Organization settings → Skills**.
2. **Zip the skill folder** so that `SKILL.md` sits at the root of the archive (not inside a nested subfolder):
   ```bash
   cd skills/finance
   zip -r stock-analysis.zip stock-analysis
   ```
3. In Claude, go to **Customize → Skills**, click **+** → **Upload a skill**, and select `stock-analysis.zip`.
4. The skill appears in your list — toggle it **on**.

Uploaded skills are private to your account.

### Claude mobile app

Custom-skill **uploading** is done from the web or desktop app (steps above) — mobile doesn't have an upload UI. Once uploaded there, the skill is tied to your account, so you can toggle and use it from the mobile app under its **Skills** settings.

## Authoring / contributing

See [`CLAUDE.md`](CLAUDE.md) for the layout and authoring conventions (frontmatter as the trigger contract, progressive disclosure via `references/`).
