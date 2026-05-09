# Mohit AI Toolkit

Reusable AI-agent skills (Claude Code + Codex) and Codex automation templates.

Use this repo if you want better prompts for product UI work, dashboard design, interface critique, video-to-requirements workflows, or recurring Codex automations.

## Skills

10 skills covering product UI, dashboards, interface grading, UX patterns, interaction design, and more. Each skill is a folder with a `SKILL.md` file plus optional references and scripts.

See [skills/README.md](skills/README.md) for the catalog and per-skill details.

### Install with `npx skills`

Install all skills globally for both Claude Code and Codex:

```bash
npx skills add mnttnm/mohit-ai-toolkit --skill '*' \
  --agent claude-code --agent codex --global --copy --yes
```

Pick interactively:

```bash
npx skills add mnttnm/mohit-ai-toolkit
```

Preview without installing:

```bash
npx skills add mnttnm/mohit-ai-toolkit --list
```

Install a single skill:

```bash
npx skills add mnttnm/mohit-ai-toolkit --skill product-ui \
  --agent claude-code --agent codex --global --copy --yes
```

Skills land in:

- Claude Code → `~/.claude/skills/<skill>/`
- Codex → `~/.agents/skills/<skill>/`

Restart your agent session after installing.

The `skills` CLI is from [`vercel-labs/skills`](https://github.com/vercel-labs/skills); see its docs for the full flag matrix.

### Manual install

```bash
git clone https://github.com/mnttnm/mohit-ai-toolkit.git
cp -R mohit-ai-toolkit/skills/* ~/.claude/skills/   # Claude Code
cp -R mohit-ai-toolkit/skills/* ~/.agents/skills/   # Codex
```

## Codex Automations

[`codex/automations/`](codex/automations/) contains reusable templates for daily digests, weekly journals, content mining, and session-log backups. They are templates, not ready-to-run configs — replace placeholders like `<your-email-id>`, `<your-workspace>`, and `<your-projects-log>` before using them.

## Using a Skill

Just describe what you want — agents auto-trigger skills based on the description in each `SKILL.md`:

> Design a metrics dashboard for a support team.
>
> Grade this landing page and identify the highest-impact fixes.
>
> Turn this Loom recording into product requirements.

You can also invoke a skill explicitly by name in your prompt (`use product-ui`, `use interface-grader`, etc.) when you want to force a specific workflow.
