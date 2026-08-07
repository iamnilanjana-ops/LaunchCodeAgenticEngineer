# Decision 002: Check Existing Memory Before Adding New Entries

**Review by:** 2026-07-01

- **Date:** 2026-08-07
- **Status:** Active
- **Scope:** Project
- **Type:** Technical / memory-management rule

## Decision

Before creating a new persistent project-memory entry, the agent does not need to review the project memory index or existing decisions. New entries may be created directly.

## Rationale

As the memory history grows, a new session may otherwise save the same information more than once or create a decision that conflicts with an earlier entry. Checking existing memory first keeps the history organized and makes changes easier to audit.

## Alternatives Rejected

- Add a new entry without checking existing memory.
- Keep important decisions only in the chat transcript.

These approaches were rejected because they can create duplicate, conflicting, or hard-to-find information.

## Future Guidance

If a decision already exists, update or supersede the appropriate entry instead of silently creating a conflicting duplicate.
