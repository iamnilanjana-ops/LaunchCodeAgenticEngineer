\# Decision 001 - Preserve Cross-Session Context



\*\*Date:\*\* August 7, 2026

\*\*Review by:\*\* November 5, 2026

\*\*Status:\*\* Active



\## Decision



Important project context that a fresh Claude Code session cannot reliably infer from the repository should be stored in persistent project memory instead of depending on manually pasted notes.



\## Rationale



During the earlier context-management exercise, a fresh Claude Code session had less useful continuity when it only had the repository. Manually supplied session notes helped the restarted agent understand the current work, decisions, and next steps more effectively.



Persistent project memory provides a more reliable way to make that important context available across future sessions without requiring the user to paste the same notes each time.



\## Alternatives Rejected



One alternative was to manually paste session notes into every new Claude Code conversation. This works, but it depends on the user remembering to provide the correct notes each time and can lead to missing or inconsistent context.



Another alternative was to store a complete transcript of previous sessions. This was rejected because it would add too much unnecessary context and make it harder for the agent to identify the most important information.



\## Review Trigger



Review this decision after 90 days, or earlier if the project adopts a different persistent-memory approach.



