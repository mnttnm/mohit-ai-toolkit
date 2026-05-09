# Skills

These skills are reusable workflow guides for AI coding agents. A skill is a folder with a `SKILL.md` file and, when useful, supporting references, scripts, or assets.

Each skill in this folder is compatible with:

- Claude-style skill folders.
- Codex-style skill folders.
- Other coding agents that can load `SKILL.md` instructions.

Each skill also includes `agents/openai.yaml` so Codex can show a display name, short description, and default prompt.

## Install

### With `npx skills`

Install all skills from this repo:

```bash
npx skills add mnttnm/mohit-ai-toolkit
```

Install one skill:

```bash
npx skills add mnttnm/mohit-ai-toolkit --skill product-ui
```

Install for selected agents:

```bash
npx skills add mnttnm/mohit-ai-toolkit --agent claude-code --agent codex
```

List available skills:

```bash
npx skills add mnttnm/mohit-ai-toolkit --list
```

### Manual Install

Copy the skill folders you want into your agent's skills directory.

Claude-style agents:

```bash
mkdir -p ~/.claude/skills
cp -R skills/product-ui ~/.claude/skills/
```

Codex:

```bash
mkdir -p ~/.codex/skills
cp -R skills/product-ui ~/.codex/skills/
```

Copy every skill:

```bash
cp -R skills/* ~/.codex/skills/
```

Restart the agent session after copying.

## Catalog

| Skill | Use it for |
| --- | --- |
| `designing-dashboards` | Designing modern, actionable dashboards through requirements, strategy, layout, chart selection, and validation. |
| `harvest-feed` | Turning a work session or conversation into publishable feed entries for a digital garden or content site. |
| `interaction-design` | Adding microinteractions, motion, loading states, transitions, and useful feedback patterns. |
| `interface-grader` | Scoring a website, app, or prototype with evidence-backed design quality criteria. |
| `lenny-research` | Researching Lenny Rachitsky-style product, growth, startup, and career topics from a structured archive. |
| `product-design-craft` | Improving interfaces with the craft level of polished products like Linear, Stripe, Figma, Notion, and Slack. |
| `product-ui` | Building production-grade product UI with strong interaction design, state handling, animation, and design tokens. |
| `ui-autoimprove` | Running iterative grade-fix-verify loops to improve frontend UI quality. |
| `ux-patterns` | Making UX decisions about navigation, hierarchy, simplification, copy, control, and information architecture. |
| `video-decompose` | Converting screen recordings or walkthrough videos into keyframes, transcripts, and requirements. |

## Example Prompts

```text
Use $designing-dashboards to design a metrics dashboard for a support team.
```

```text
Use $product-ui to improve this SaaS settings page without changing the backend behavior.
```

```text
Use $interface-grader to evaluate this prototype and give me the top fixes.
```

```text
Use $ui-autoimprove to run one improvement cycle on this frontend.
```

```text
Use $video-decompose to extract requirements from this Loom recording.
```

## Skill Structure

Each skill follows this shape:

```text
skill-name/
  SKILL.md
  agents/openai.yaml
  references/        # optional
  scripts/           # optional
  assets/            # optional
```

`SKILL.md` is the main instruction file. References are loaded only when the workflow needs more detail. Scripts are included when a workflow benefits from deterministic tooling.
