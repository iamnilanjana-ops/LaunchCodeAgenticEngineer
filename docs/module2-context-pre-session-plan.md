\# Module 2 Context Management Pre-Session Plan



\## Exercise



Module 2, Lesson 2, Exercise 2.2: Manage Context in a Long-Running Agent Session



\## Target Codebase



React Art \& Craft Marketplace



\## Repository



LaunchCodeAgenticEngineer



\## Real Project Task



The agent will review the Art \& Craft Marketplace project and create a prioritized recommendation for improving the project before further development.



The review will focus on:



\* build status;

\* current warnings;

\* code-quality concerns;

\* existing modified files;

\* and project readiness.



This is a real task because the project has previously produced build warnings and has contained pre-existing modified files that were not reviewed by the agent.



\## Agent Used



I will use the existing project review agent.



The agent can inspect the project, run the build, review Git status, identify issues, and provide recommendations without modifying project files.



\## Phase 1: Initial Project Review



During Phase 1, the agent will:



1\. Run `git status`.

2\. Run `npm run build`.

3\. Separate errors from warnings.

4\. Review the available project information.

5\. Create an initial prioritized recommendation.



\### Active Phase 1 Requirements



\* Do not modify any project files.

\* Clearly separate errors and warnings.

\* Report the build result accurately.

\* Do not confirm overall project readiness when unreviewed modified files exist.

\* Prioritize build and Git-safety concerns.



\## Planned Requirement Change



After Phase 1, I will introduce a new requirement.



The new requirement will state that accessibility concerns must be treated as a higher priority than optional dependency or maintenance warnings.



This means the agent must reconsider its original recommendation and update the priority order.



\## Phase 2: Revised Review



During Phase 2, the agent will:



1\. Review the initial recommendation.

2\. Apply the new accessibility-priority requirement.

3\. Reassess the project findings.

4\. Produce a revised final recommendation.



\### Active Phase 2 Requirements



\* All Phase 1 safety requirements remain active.

\* Do not modify project files.

\* Accessibility concerns must be prioritized above optional dependency or maintenance warnings.

\* The final recommendation must reflect the newest requirement.

\* The agent must not continue using the outdated Phase 1 priority order.



\## Artifact the Agent Will Revisit



The agent will revisit its initial prioritized project recommendation.



It must update the recommendation after the accessibility-priority requirement is introduced.



\## Context Boundary



The main context boundary will occur after the initial recommendation is completed and before the accessibility requirement is introduced.



At this boundary, I will tell the agent:



\* Phase 1 is complete.

\* Phase 2 is beginning.

\* Existing safety requirements remain active.

\* The priority requirement has changed.

\* The initial recommendation must be revisited.



\## Proactive Summary Point



I will request a proactive summary after introducing the new requirement and before asking for the final revised recommendation.



The summary must preserve:



\* the current goal;

\* active requirements;

\* the new accessibility-priority rule;

\* decisions made during Phase 1;

\* the current initial recommendation;

\* unresolved questions;

\* and the next action.



\## Evidence Used to Evaluate the Session



I will evaluate the session using:



\* the Phase 1 recommendation;

\* the proactive summary;

\* the Phase 2 revised recommendation;

\* Git status output;

\* build output;

\* specific statements showing whether the agent followed the newest requirement;

\* and any evidence of outdated or conflicting recommendations.



\## Evaluation Questions



I will check whether the agent:



1\. Used the current project facts accurately.

2\. Followed the requirement change.

3\. Updated the earlier recommendation.

4\. Preserved active safety constraints.

5\. Avoided relying on outdated requirements.

6\. Produced one coherent final recommendation.



\## Expected Context-Management Risk



The main risk is that the agent may remember the initial priority order and continue treating build-maintenance warnings as more important than accessibility concerns.



This task should reveal whether an explicit context boundary and proactive summary help the agent apply the newest requirement consistently.



