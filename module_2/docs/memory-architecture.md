\# Memory Architecture



\## What this workflow needs to remember



This project uses Claude Code across multiple sessions for Agentic Engineer assignments. A fresh session needs to remember important project decisions, current work state, known limitations, and stable rules that may not be obvious from the repository alone. Information that is already available in code, Git history, or existing documentation does not need to be duplicated. Temporary errors, one-time observations, credentials, passwords, personal data, and other sensitive information should not be stored in persistent memory.



\## Layer 1: Project Memory



\*\*Location:\*\* `.memory/project/`



This layer stores information that may change as the project develops.



\### Belongs here



\* Important decisions made during Agentic Engineer assignments.

\* Current project priorities or unfinished work.

\* Known limitations that future sessions need to understand.

\* Deferred tasks or next recommended actions.

\* Decisions that a fresh session cannot reliably infer from the repository.



\### Does not belong here



\* Passwords, API keys, credentials, or personal information.

\* Temporary error messages that only matter during one session.

\* Step-by-step procedures that should be stored as skills.

\* Information already clearly available in code or Git history.



\### Scope



This memory is scoped to the `LaunchCodeAgenticEngineer` Module 2 project.



\### Write permissions



Claude Code may create or update project-memory entries when an important project decision or project-state change needs to persist across sessions.



\### Pruning policy



Project-memory entries should be reviewed every 90 days. An entry should be updated or archived when a newer decision replaces it or when the related work is completed.



\## Layer 2: Knowledge Files



\*\*Location:\*\* `.memory/knowledge/`



This layer contains stable rules and standards that should guide the agent across many sessions.



\### Belongs here



\* Coding and documentation standards.

\* Rules for safe Git usage.

\* Project-specific constraints.

\* Standards for how agents should modify files.

\* Rules that should only change after human review.



\### Does not belong here



\* Temporary project status.

\* Current assignment progress.

\* Session-specific errors.

\* Decisions that may change frequently.



\### Scope



These standards apply to the Module 2 project.



\### Write permissions



Knowledge Files are human-maintained and read-only for the agent. Claude Code may read these files but should not modify them.



\### Pruning policy



Knowledge Files should be reviewed when project standards change or during a scheduled review. A human must approve any changes.



\## Layer 3: Indexed Reference Documents



\*\*Location:\*\* `.memory/reference/`



This layer is intended for larger or less frequently needed reference documents.



At this time, the project does not require additional reference documents because the important course notes and project documentation are already available in the repository.



The `.memory/reference/` folder and `MEMORY\_INDEX.md` will still be maintained so reference documents can be added later if the project grows.



A reference document should be added in the future if there are several large design documents, previous reports, meeting notes, or other background documents that would be inefficient to load during every session.



\### Write permissions



Reference documents are human-maintained and should be treated as read-only by the agent.



\### Pruning policy



Reference documents should be reviewed when they are replaced, become outdated, or are no longer useful to the project.



\## Allocation Decision



A repeatable procedure, such as the commands for running tests or preparing a Git commit, should not be stored in project memory. It belongs in a skill because it describes how to perform a task rather than information the project needs to remember.



Temporary errors and observations should remain in the current session because they do not need to survive after the problem is solved.



Credentials, passwords, API keys, personal data, and other sensitive information must never be stored in any memory layer.



\## Alternatives Considered



I considered storing step-by-step Git and testing instructions in Project Memory because they may be useful in future sessions. I decided not to store them there because they are repeatable procedures. They belong in skills, while Project Memory should stay focused on changing project state and important decisions.



