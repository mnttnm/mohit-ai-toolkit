# Mohit AI Toolkit

A public collection of reusable AI-agent skills and Codex automation templates.

Use this repo if you want better prompts for product UI work, dashboard design, interface critique, video-to-requirements workflows, or recurring Codex automations.

## What Is Included

### Skills

Skills are small folders that teach an AI coding agent a specialized workflow. Each skill has a `SKILL.md` file, and some include supporting references, scripts, or assets.

The skills in this repo are adapted for agents that understand `SKILL.md` folders, including Claude-style and Codex-style setups. Each skill also includes Codex UI metadata at `agents/openai.yaml`.

See [skills/README.md](skills/README.md) for the full catalog.

### Codex Automations

The `codex/automations` folder contains reusable Codex automation templates for recurring workflows such as:

- Daily Codex work digests.
- Weekly content mining from Codex sessions.
- Agent session log backups.
- Weekly work journals.

These are templates, not ready-to-run personal configs. Replace placeholders such as `<your-email-id>`, `<your-workspace>`, `<your-projects-log>`, and `<your-client-name>` before using them.

## Install Skills

### With `npx skills`

Install interactively from GitHub with the `skills` CLI:

```bash
npx skills add mnttnm/mohit-ai-toolkit
```

Install all skills globally for Claude Code and Codex without prompts:

```bash
npx skills add mnttnm/mohit-ai-toolkit --skill '*' --agent claude-code --agent codex --global --copy --yes
```

Install a specific skill globally:

```bash
npx skills add mnttnm/mohit-ai-toolkit --skill product-ui --agent claude-code --agent codex --global --copy --yes
```

Install for only Claude Code:

```bash
npx skills add mnttnm/mohit-ai-toolkit --skill product-ui --agent claude-code --global --copy --yes
```

Install for only Codex:

```bash
npx skills add mnttnm/mohit-ai-toolkit --skill product-ui --agent codex --global --copy --yes
```

List the available skills without installing:

```bash
npx skills add mnttnm/mohit-ai-toolkit --list
```

The `skills` CLI supports multiple coding agents, including Claude Code and Codex. For global installs, Claude Code receives skills under `~/.claude/skills`, while Codex receives them under `~/.agents/skills`. See the [`vercel-labs/skills`](https://github.com/vercel-labs/skills) project for CLI details.

### Manual Install

Clone the repo if you prefer to copy folders yourself:

```bash
git clone https://github.com/mnttnm/mohit-ai-toolkit.git
cd mohit-ai-toolkit
```

### Claude-Style Agents

Copy one skill into your skills directory:

```bash
cp -R skills/product-ui ~/.claude/skills/
```

Or copy all skills:

```bash
mkdir -p ~/.claude/skills
cp -R skills/* ~/.claude/skills/
```

### Codex

Copy one skill into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R skills/product-ui ~/.codex/skills/
```

Or copy all skills:

```bash
mkdir -p ~/.codex/skills
cp -R skills/* ~/.codex/skills/
```

Restart your agent session after copying so the skills are rediscovered.

## Use A Skill

Invoke a skill by name in your prompt:

```text
Use $designing-dashboards to design a metrics dashboard for a support team.
```

```text
Use $product-ui to redesign this dashboard so it feels polished and production-ready.
```

```text
Use $interface-grader to score this landing page and identify the highest-impact fixes.
```

```text
Use $video-decompose to turn this screen recording into product requirements.
```

Agents may also auto-trigger skills when the skill description matches your request.

## Use Automation Templates

Copy an automation template into your Codex automation setup, then replace placeholders:

```bash
cp -R codex/automations/codex-morning-digest ~/.codex/automations/
```

Before running an automation, review its `automation.toml` and fill in your own paths, email, repo names, deployment settings, and workspace locations.
