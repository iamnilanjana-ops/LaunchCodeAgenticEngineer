\# Project Memory Index



Claude Code should use this index to locate important project memory that may not be reliably inferred from the repository alone.



\## Active Decisions



\### Decision 001 - Preserve Cross-Session Context



\*\*File:\*\* `decisions/decision-001.md`



\*\*Use when:\*\* Starting a fresh session or resuming Module 2 work across sessions.



\*\*Summary:\*\* Important project context that cannot be reliably inferred from the repository should be preserved in structured persistent memory rather than depending on manually pasted conversation notes.



\*\*Status:\*\* Active



\### Decision 002 - Check Existing Memory Before Adding New Entries



\*\*File:\*\* `decisions/decision-002.md`



\*\*Use when:\*\* Before creating a new persistent project-memory entry.



\*\*Summary:\*\* Check the existing memory index and relevant decisions before creating a new memory entry, to avoid duplicates or conflicts.



\*\*Status:\*\* Active



\### Decision 003 - Keep Stable Knowledge Read-Only



\*\*File:\*\* `decisions/decision-003.md`



\*\*Use when:\*\* Before reading or considering any change to files in `.memory/knowledge/`.



\*\*Summary:\*\* Files in `.memory/knowledge/` are human-maintained and read-only for the agent; content and permissions must not be changed without explicit human instruction.



\*\*Status:\*\* Active



\### Decision 004 - Store Evolving Decisions in Project Memory



\*\*File:\*\* `decisions/decision-004.md`



\*\*Use when:\*\* Deciding where to record project context or decisions that cannot be inferred from the repository.



\*\*Summary:\*\* Evolving project decisions belong in `.memory/project/decisions/`; stable reusable guidance stays in the knowledge layer, and reference material stays in the reference layer.



\*\*Status:\*\* Active



\## Canonical Index

This file is the single canonical Project Memory index; CLAUDE.md directs fresh sessions to read it at startup. Do not create another `MEMORY_INDEX.md` anywhere under `.memory/project/` (including inside `decisions/`) — a second index list would duplicate this one and could drift out of sync. If a subfolder ever needs a quick-reference list, link back to this file instead of copying its contents.



\## Usage



At the start of a fresh session:



1\. Review this index.

2\. Read relevant decision entries before making project decisions.

3\. Use the entries as additional context alongside the actual repository.

4\. Do not invent decisions that are not documented in the memory files.

5\. If an entry appears outdated or conflicts with the current repository, report the conflict instead of silently relying on the memory.



