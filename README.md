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

Clone the repo:

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

## Public-Safety Notes

The examples are sanitized for public sharing:

- No real API keys, access tokens, passwords, or private keys.
- No personal local paths.
- No private repository names.
- No client names or internal project identifiers.
- No real Codex thread IDs.

Treat the automation files as templates. Do not paste private session logs, credentials, or client-specific paths into a public fork.

