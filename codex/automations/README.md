# Codex Automation Templates

Reusable Codex automation templates. Each template is a TOML file that the Codex app loads as a scheduled task — Codex wakes up on the configured schedule, runs the prompt, and surfaces the result in your Triage.

These templates are sanitized: no real credentials, paths, client names, or internal URLs. Replace the placeholders, then activate.

## What's in this folder

| Template | Kind | Default schedule | Use it for |
| --- | --- | --- | --- |
| [`codex-morning-digest`](codex-morning-digest/) | `cron` | Daily 08:00 | Plain-text email summary of yesterday's Codex work plus today's priorities. Generates a rendered HTML digest, Markdown report, and archives a copy to a private repo. |
| [`weekly-codex-content-mining`](weekly-codex-content-mining/) | `cron` | Friday 17:00 | Mines the past week's Codex sessions across one or more workspaces and drafts shareable content suggestions. |
| [`backup-agent-session-logs`](backup-agent-session-logs/) | `cron` | Daily 00:00 | Backs up Codex and Claude Code session logs to a private repo so they survive session rotation. |
| [`weekly-work-journal`](weekly-work-journal/) | `heartbeat` | Sunday 18:00 | Wakes a long-running Codex journal thread each Sunday and continues the conversation in-thread. |

## Two kinds of automations

- **Standalone** (`kind = "cron"`) — fresh run each time. Reports to your Triage. Best for digests, weekly reports, scheduled scans.
- **Thread heartbeat** (`kind = "heartbeat"`) — attaches to an existing Codex thread (`target_thread_id`) and continues that conversation on a schedule. Best for ongoing follow-up loops in a long-running thread.

## Install

Copy the template folder into your Codex automations directory:

```bash
mkdir -p ~/.codex/automations
cp -R codex/automations/codex-morning-digest ~/.codex/automations/
```

Open the file and replace placeholders:

```bash
$EDITOR ~/.codex/automations/codex-morning-digest/automation.toml
```

Restart the Codex app so it picks up the new automation. You should see it listed in the Codex automations panel; flip `status = "ACTIVE"` once you're ready to let it run on schedule.

## Placeholders to replace

Every template uses angle-bracket placeholders. Search for `<` in the file to find them all. Common ones:

| Placeholder | Replace with |
| --- | --- |
| `<your-email-id>` | Email address that should receive output. |
| `<your-workspace>` | Absolute path to the workspace the automation runs in. `cwds` is an array — list one or more. |
| `<your-projects-log>` | Absolute path to a private repo where reports get archived. |
| `<your-digest-output-folder>` | Absolute path where local HTML/Markdown artifacts land. |
| `<your-marketing-workspace>` | Absolute path to a workspace mined for content ideas. |
| `<your-session-log-backup-repo>` | Absolute path to the private repo backing up session logs. |
| `<your-client-name>` | Real client/project name for filtering or routing. |
| `<codex-thread-id>` | UUID of an existing Codex thread (heartbeat automations only — open the thread in Codex and copy from the URL). |

The prompts also reference internal links, deployment targets, and email routing rules. Read the prompt before activating — these run unattended.

## TOML schema reference

| Field | Required for | Notes |
| --- | --- | --- |
| `version` | all | Schema version, currently `1`. |
| `id` | all | Unique identifier; matches the folder name. |
| `kind` | all | `"cron"` (standalone) or `"heartbeat"` (thread). |
| `name` | all | Human-readable name shown in the Codex UI. |
| `prompt` | all | Instructions Codex runs each time the automation fires. |
| `status` | all | `"ACTIVE"` to enable; anything else pauses the schedule. |
| `rrule` | all | [RFC 5545](https://datatracker.ietf.org/doc/html/rfc5545#section-3.3.10) recurrence rule, e.g. `FREQ=WEEKLY;BYDAY=FR;BYHOUR=17;BYMINUTE=0`. |
| `model` | cron | Model identifier, e.g. `gpt-5.5`. |
| `reasoning_effort` | cron | `"low"`, `"medium"`, or `"high"`. |
| `execution_environment` | cron | `"local"` or `"worktree"`. Use `worktree` if the automation makes git commits. |
| `cwds` | cron | Array of absolute paths the automation can operate in. |
| `target_thread_id` | heartbeat | UUID of the thread the heartbeat attaches to. |

`created_at` and `updated_at` are populated automatically once Codex registers the automation — don't set them in templates.

## Safety

These automations run **unattended** on the schedule you set. Before flipping `status` to `ACTIVE`, audit the prompt for:

- **Side effects** — commands that push, deploy, send email, or post to Slack. Confirm every destination is yours.
- **Scope** — `cwds` controls what files the automation can touch. Keep it tight.
- **Stale placeholders** — a leftover `<your-email-id>` won't fail loudly; it'll just send mail to nowhere or to the wrong place.

If you fork these templates and share them, scrub real paths, emails, repo URLs, and client names first.
