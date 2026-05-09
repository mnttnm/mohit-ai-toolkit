# Mohit AI Toolkit

Reusable prompts, automation templates, skills, and operating patterns for AI-assisted work.

Everything in this repo is intended to be public-safe. Local paths, personal account names,
private repository names, client names, thread IDs, and credential-shaped values are replaced
with placeholders.

## Codex Automations

The `codex/automations` folder contains sanitized Codex automation templates. They are written as public-safe examples and intentionally use placeholders instead of private paths, account names, repository names, client names, thread IDs, tokens, or email addresses.

Before using a template, replace placeholders such as `<your-email-id>`, `<your-projects-log>`, `<your-workspace>`, and `<your-client-name>` with your own local values.

## Skills

The `skills/` folder contains the 10 skills already published in
[`mnttnm/claude-skills`](https://github.com/mnttnm/claude-skills), adapted for broader agent compatibility.

Each published skill includes:
- A normalized `SKILL.md` with `name` and `description` frontmatter.
- Any required `references/`, `scripts/`, or `assets/`.
- Codex UI metadata at `agents/openai.yaml`.

This repo intentionally does not mirror all locally installed agent, Claude, or Codex skills.
See `skills/README.md` for the skill index.
