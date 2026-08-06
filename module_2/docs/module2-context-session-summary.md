\# Module 2 Context-Management Session Summary



\## Exercise



Module 2, Lesson 2, Exercise 2.2: Manage Context in a Long-Running Agent Session



\## Agent Used



Build Review Agent v1.1



\## Target Codebase



Art \& Craft Marketplace React project



\## Session Goal



The goal was to perform a multi-phase, read-only project review and test whether the agent could maintain the correct context after a requirement changed.



\---



\## Phase 1: Initial Review



The agent performed a read-only review of the project.



\### Confirmed Build Findings



\* The React production build succeeded.

\* No build errors were reported.

\* No build warnings were reported.

\* JavaScript bundle size: 76.36 kB gzipped.

\* CSS bundle size: 1.07 kB gzipped.

\* The agent did not intentionally modify project files.



\### Git Status Finding



Before the container session, the host PowerShell `git status` showed one modified file:



`docs/module2-iteration-log.md`



During Phase 1, the agent reported 30 pre-existing modified/uncommitted files.



This created a conflict between the host observation and the agent's observation.



\### Initial Recommendation



The agent correctly followed its Recommendation Guardrail and did not confirm overall project readiness.



Its initial priorities were:



1\. Review modified source files.

2\. Review modified documentation and configuration files.

3\. Commit or discard reviewed changes.

4\. Treat the browserslist/caniuse-lite update as optional and low priority.



\---



\## Explicit Context Boundary



After Phase 1, an explicit context boundary was introduced.



The agent was told:



\* Phase 1 was complete.

\* Phase 2 was beginning.

\* Existing read-only and Git-safety requirements remained active.

\* The Git-status conflict must remain unresolved rather than being silently corrected.

\* The Phase 1 recommendation must be revisited.



A new requirement was then introduced:



\*\*Accessibility concerns must be prioritized above optional dependency or maintenance warnings.\*\*



\---



\## Proactive Summary



Before producing the Phase 2 recommendation, the agent was asked to summarize the current session state.



The summary preserved:



\* the current project-review goal;

\* the active read-only requirement;

\* the requirement to separate errors from warnings;

\* the Git-safety guardrail;

\* the new accessibility-priority requirement;

\* the Phase 1 build findings;

\* the initial recommendation;

\* the conflicting Git-status observations;

\* unresolved questions;

\* and the next planned action.



\### Important Unresolved Issue



The agent explicitly preserved the following inconsistency:



\* Host PowerShell reported one modified file.

\* The agent reported 30 modified files.



The agent did not silently choose one observation as correct.



It identified possible causes such as environment, working-tree state, timing, or path differences but did not claim that any one cause was proven.



\---



\## Phase 2: Revised Recommendation



The agent revised the original recommendation after the accessibility requirement changed.



\### Revised Priorities



1\. Resolve the Git-status discrepancy using current evidence.

2\. Review accessibility-related aspects of modified UI files.

3\. Review remaining documentation and configuration changes.

4\. Treat the optional browserslist/caniuse-lite update as the lowest priority.



The agent did not claim that an accessibility defect existed. Instead, it correctly described accessibility as an unreviewed area that now had higher priority.



The agent also continued to state that overall project readiness could not be confirmed.



\---



\## What Changed Between Phase 1 and Phase 2



The Phase 1 recommendation did not specifically prioritize accessibility.



After the requirement change, the agent:



\* added accessibility review as a high-priority action;

\* placed accessibility above optional maintenance work;

\* moved the browserslist/caniuse-lite update to the lowest priority;

\* preserved the Git-status discrepancy as unresolved;

\* and avoided inventing an accessibility defect without evidence.



\---



\## Context Drift / Misfire Observed



The main misfire was the conflicting Git-status information.



The host environment showed one modified file, while the agent reported 30 modified files.



Instead of restarting the session, the discrepancy was carried forward as an unresolved issue, as required by the exercise.



The explicit context boundary and proactive summary helped prevent this inconsistency from being forgotten during Phase 2.



\---



\## Compaction



Compaction was not used.



The session remained manageable with an explicit context boundary and proactive summarization. There was no clear need to compact the context.



\---



\## Initial Evaluation



\### Accuracy



\*\*Score: 3/4\*\*



The agent accurately reported the build result, errors, warnings, and bundle sizes. However, the Git-status observation conflicted with the host PowerShell baseline, so the session did not have fully consistent project-state evidence.



\### Task Adherence



\*\*Score: 4/4\*\*



The agent followed the read-only requirements, preserved the safety guardrail, responded correctly to the requirement change, and prioritized accessibility above optional maintenance work in Phase 2.



\### Coherence



\*\*Score: 4/4\*\*



The proactive summary preserved the current requirements and unresolved Git-status conflict. The Phase 2 recommendation clearly revised the Phase 1 recommendation rather than reverting to the old priority order.



\---



\## Context-Management Choice for a Future Run



In a future run, I would verify the host and container Git status immediately at the beginning of the session and record both outputs before asking the agent to make recommendations.



This would establish a clearer shared baseline and reduce uncertainty about whether the agent is using stale or environment-specific project information.



