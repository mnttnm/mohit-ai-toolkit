# Skills

Reusable workflow guides for AI coding agents. Each skill is a folder with a `SKILL.md` file plus optional `references/`, `scripts/`, or `assets/`. Skills work with Claude Code, Codex, and any other agent that loads `SKILL.md` instructions.

## Install

See the top-level [README](../README.md#install-with-npx-skills) for full install commands. Quick reference:

```bash
# Everything, both agents, global
npx skills add mnttnm/mohit-ai-toolkit --skill '*' \
  --agent claude-code --agent codex --global --copy --yes

# One skill
npx skills add mnttnm/mohit-ai-toolkit --skill product-ui \
  --agent claude-code --agent codex --global --copy --yes

# List without installing
npx skills add mnttnm/mohit-ai-toolkit --list
```

Install paths:

- Claude Code → `~/.claude/skills/<skill>/`
- Codex → `~/.agents/skills/<skill>/`

When using `--skill <name>`, use the skill's frontmatter `name` (the identifier shown in `--list`), not the folder name. For this repo they match for every skill.

## Catalog

| Skill | Use it for |
| --- | --- |
| `designing-dashboards` | Designing modern, actionable dashboards through requirements, strategy, layout, chart selection, and validation. |
| `ecommerce-conversion-audit` | Auditing ecommerce PDPs, home pages, nudges, offers, trust signals, and data readiness for faster purchase decisions. |
| `harvest-feed` | Turning a work session into publishable feed entries for a digital garden. |
| `interaction-design` | Microinteractions, motion, loading states, transitions, and feedback patterns. |
| `interface-grader` | Scoring a website, app, or prototype with evidence-backed design criteria. |
| `lenny-research` | Researching Lenny Rachitsky-style product, growth, startup, and career topics from a structured archive. |
| `product-design-craft` | Improving interfaces with the craft level of Linear, Stripe, Figma, Notion, and Slack. |
| `product-ui` | Building production-grade product UI with strong interaction design, state handling, animation, and design tokens. |
| `ui-autoimprove` | Iterative grade-fix-verify loops to improve frontend UI quality. |
| `ux-patterns` | UX decisions about navigation, hierarchy, simplification, copy, control, and information architecture. |
| `video-decompose` | Converting screen recordings into keyframes, transcripts, and requirements. |

## Skill structure

```
skill-name/
  SKILL.md           # main instructions; frontmatter with name + description
  references/        # optional, loaded only when needed (progressive disclosure)
  scripts/           # optional, deterministic tooling
  assets/            # optional
```

`SKILL.md` is the only file every skill must have. Both Claude Code and Codex read its frontmatter (`name`, `description`) for auto-triggering.
