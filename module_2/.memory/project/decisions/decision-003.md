# Decision 003: Keep Stable Knowledge Read-Only

**Review by:** 2026-11-05

- **Date:** 2026-08-07
- **Status:** Active
- **Scope:** Project
- **Type:** Technical / permission rule

## Decision
Files in `.memory/knowledge/` are treated as human-maintained, read-only knowledge. The agent may read and use them, but it must not change their permissions or content unless a human explicitly instructs it to do so.

## Rationale
Stable knowledge should not change accidentally during normal agent work. Separating writable project decisions from protected knowledge makes the memory system safer and more reliable across sessions.

## Alternatives Rejected
- Allow the agent to edit knowledge files automatically.
- Store all project and knowledge memory in one writable folder.

These approaches were rejected because an agent could accidentally overwrite trusted information or make stable knowledge inconsistent.

## Future Guidance
When stable knowledge needs to change, the agent should identify the issue and wait for explicit human instruction before modifying the knowledge layer.
