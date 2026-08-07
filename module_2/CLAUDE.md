# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Docker-based development environment for LaunchCode's **Agentic Programming** course, Module 2. It extends the Module 1 environment with MCP (Model Context Protocol) server support for Slack and Gmail, plus pre-configured Claude Code skills.

## MCP Servers

Two MCP servers are pre-installed and configured in `/root/.claude/settings.json`:

### Slack
- Package: `@modelcontextprotocol/server-slack`
- Requires env vars: `SLACK_BOT_TOKEN`, `SLACK_TEAM_ID`
- Allows Claude Code prompts to read channels, post messages, and interact with Slack workspaces.

### Gmail
- Package: `@gongrzhe/server-gmail-autoauth-mcp`
- OAuth credentials stored in `/root/.gmail-mcp/` (persist this directory across container runs if needed)
- Allows Claude Code prompts to read, search, and send Gmail messages.

## Skills

Pre-configured skills (invoked with `/skill-name` in Claude Code):

| Skill | Description |
|---|---|
| `/send-slack-message` | Send a message to a Slack channel |
| `/check-gmail` | Summarize recent unread Gmail messages |
| `/send-email` | Draft and send an email via Gmail |
| `/summarize-session` | Bullet-point summary of the current session |

Skills are defined in `settings.json` which is copied to `/root/.claude/settings.json` during image build.

## Session Continuity

Before starting work, read `docs/session-notes.md` for context from the previous session.
At the end of a session, append a new entry summarizing what was done and what's next.

## Agents

Pre-configured sub-agents available inside Claude Code sessions. Agents are autonomous specialists that Claude Code can invoke automatically or that you can request explicitly.

| Agent | Description |
|---|---|
| `code-reviewer` | Reviews recent git changes for quality, security, and maintainability |
| `email-summarize` | Checks new Gmail messages and posts sender + 2-line summary to #test Slack channel |

Agents are defined as Markdown files with YAML frontmatter in `/root/.claude/agents/` inside the container. Source files live in the `agents/` directory of this repo and are copied in at build time.

**Running an agent:**

Ask Claude Code to use the agent explicitly:
```
Review my recent changes using the code-reviewer agent.
```

Or Claude Code may invoke it automatically when the task matches the agent's description.

## Running Streamlit Apps

From inside the container:
```bash
streamlit run app.py
```

Access at `http://localhost:8501`.

## Key Dependencies (requirements.txt)

- `anthropic` — Claude API client
- `streamlit` — web UI framework
- `python-dotenv` — environment variable management
- `slack_sdk` — Slack integration (Python)
- `google-api-python-client`, `google-auth-oauthlib` — Gmail/Google API access (Python)
- `fastapi`, `flask`, `uvicorn` — web frameworks
- `pydantic`, `httpx` — HTTP and data validation

## Environment & Tools in the Container

- Python 3.12 (aliased as `python` and `pip`)
- Claude Code CLI (`claude`) installed globally via npm
- OpenCode (`opencode-ai`) installed globally via npm
- MCP server: `@modelcontextprotocol/server-slack`
- MCP server: `@gongrzhe/server-gmail-autoauth-mcp`
- ngrok for tunneling
- Workspace mounted at `/workspace`

## Gmail API Setup

Place `credentials.json` (from Google Cloud Console) in your workspace directory. On first run it triggers OAuth and saves `token.json`. Both files should be in `.gitignore`.

## Persistent Memory System

At the start of every fresh session:

1. Read `.memory/project/MEMORY_INDEX.md`.
2. Read any active Project Memory entries that are relevant to the current task.
3. Read `.memory/knowledge/coding-standards.md` before writing, reviewing, or modifying project files.
4. Read `.memory/reference/MEMORY_INDEX.md` to determine whether any indexed reference documents are relevant.
5. Use persistent memory only for information that is actually recorded in these files. Do not invent or assume undocumented project decisions.

### Memory Write Policy

* `.memory/project/` contains changing project context, decisions, priorities, limitations, and deferred work. Claude Code may create or update entries here when important project state changes.
* Before creating a new Project Memory entry, check `.memory/project/MEMORY_INDEX.md` for an existing entry on the same topic.
* Update the Project Memory Index whenever a Project Memory entry is created, updated, archived, or replaced.
* `.memory/knowledge/` is human-maintained and read-only for Claude Code. Never modify files in this directory.
* Never change permissions on `.memory/knowledge/` unless a human explicitly instructs you to do so.
* `.memory/reference/` contains human-maintained indexed reference material and should be treated as read-only.
* If a write to a read-only memory directory fails with a permission error, stop and report the problem instead of changing permissions.

### Memory Safety and Review

* Never store passwords, API keys, credentials, personal data, or other sensitive information in persistent memory.
* If a Project Memory entry conflicts with the current repository or appears outdated, report the conflict before relying on it.
* Project Memory entries should be reviewed according to the review trigger recorded in the entry.
* Knowledge Files should only be changed after human review.

### Stale Memory Policy

Before acting on any Project Memory entry, check its `Review by` date.

If the review date has passed:

1. Do not act on that memory entry yet.
2. Clearly report that the entry is expired.
3. Ask the human to confirm whether the entry is still accurate.
4. Wait for confirmation before using the entry.

If an expired entry also conflicts with the current repository state, treat the repository as the stronger evidence and report the conflict.

This policy applies to entries in `.memory/project/`.
