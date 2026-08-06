\# Module 2 Context-Management Technique Plan



\## Exercise



Module 2, Lesson 2, Exercise 2.2: Manage Context in a Long-Running Agent Session



\## Session Goal



The agent will review the Art \& Craft Marketplace project in two phases and revise its recommendation after a project requirement changes.



The session will test whether the agent can:



\* remember current project facts;

\* preserve active safety requirements;

\* recognize when an earlier requirement is no longer current;

\* update an earlier recommendation;

\* and produce one coherent final result.



\## Technique 1: Explicit Context Boundary



\### Planned Location



The first explicit context boundary will occur after the agent completes the Phase 1 project review and provides its initial prioritized recommendation.



\### Boundary Message



I will tell the agent:



> Phase 1 is complete. We are now beginning Phase 2. Continue following the existing requirements to avoid modifying files, separate warnings from errors, and avoid confirming overall readiness when unreviewed changes exist. A new requirement is now active: accessibility concerns must be prioritized above optional dependency or maintenance warnings. Revisit the initial recommendation using this updated priority.



\### Why This Boundary Is Needed



This boundary clearly separates the original review from the revised review.



It reduces the risk that the agent will continue applying the Phase 1 priority order after the requirement changes. It also reminds the agent which earlier requirements remain active.



\## Technique 2: Proactive Summarization



\### Planned Location



I will request a proactive summary after introducing the new accessibility-priority requirement and before asking the agent to produce the final revised recommendation.



\### Summary Request



I will ask the agent:



> Before continuing, summarize the current session state. Include the current goal, active requirements, the requirement that changed, decisions made during Phase 1, the current recommendation that must be revised, unresolved questions, and the next planned action. Do not make the final recommendation yet.



\### Information the Summary Must Preserve



The summary must preserve:



\* the current project-review goal;

\* the instruction not to modify project files;

\* the requirement to separate errors from warnings;

\* the Git-safety requirement;

\* the new accessibility-priority requirement;

\* the main findings from Phase 1;

\* the initial recommendation;

\* the artifact that must be revisited;

\* any unresolved project questions;

\* and the next action.



\### Why Summarization Is Needed



The summary will create a compact checkpoint before the final decision.



It should make outdated requirements easier to detect and reduce the chance that the agent will overlook the new accessibility-priority rule when revising the recommendation.



\## Technique 3: Re-State Active Requirements



\### Planned Location



I will restate the active requirements at the beginning of Phase 2 and again when requesting the final revised recommendation.



\### Requirements to Re-State



The agent must:



\* not modify files;

\* use current project evidence;

\* clearly separate warnings from errors;

\* avoid confirming overall readiness when unreviewed changes exist;

\* prioritize accessibility concerns above optional dependency or maintenance warnings;

\* and revise the earlier recommendation instead of creating an unrelated new review.



\### Why This Technique Is Needed



Some Phase 1 requirements remain active while one priority requirement changes.



Re-stating the complete active requirement set should prevent the agent from treating the new requirement as a replacement for every earlier instruction.



\## Technique 4: Artifact Reference



\### Planned Location



When moving into Phase 2, I will directly identify the artifact that must be revised: the Phase 1 prioritized recommendation.



\### Planned Instruction



I will tell the agent:



> Revisit the exact recommendation you produced in Phase 1. Identify which priorities must move, remain, or be rewritten because of the new accessibility requirement.



\### Why This Technique Is Needed



Naming the exact artifact reduces the risk that the agent will forget the earlier recommendation or create a separate answer that conflicts with it.



It also makes it easier to evaluate whether the agent truly updated its previous decision.



\## Compaction Decision



I do not plan to use compaction automatically.



I will use compaction only if the session becomes crowded enough that the agent begins losing track of earlier decisions, requirements, or artifacts.



\### Why Compaction Is Not Planned Initially



The exercise requires a multi-phase session, but it does not require deliberately filling the context window.



An explicit boundary and proactive summary should be enough for this planned run. Unnecessary compaction could remove useful detail from the session.



\## Evidence to Save



I will save the following evidence from the session:



1\. The Phase 1 project findings.

2\. The Phase 1 prioritized recommendation.

3\. The explicit context-boundary message.

4\. The proactive summary.

5\. The Phase 2 revised recommendation.

6\. Git status and build output.

7\. Any moment where the agent used an outdated requirement.

8\. Any correction or recovery made by the agent.



\## Evaluation Approach



\### Accuracy



I will evaluate whether the agent correctly used:



\* Git status;

\* build results;

\* project warnings;

\* accessibility findings;

\* and the current state of the recommendation.



\### Task Adherence



I will evaluate whether the agent:



\* followed the Phase 1 requirements;

\* recognized the requirement change;

\* retained the still-active safety requirements;

\* and applied the new accessibility priority in Phase 2.



\### Coherence



I will evaluate whether:



\* the proactive summary matches the current session state;

\* the revised recommendation updates the Phase 1 recommendation;

\* and the final result reflects one consistent set of active requirements.



\## Expected Failure Modes



Possible context-management failures include:



\* continuing to prioritize maintenance warnings above accessibility;

\* forgetting the instruction not to modify files;

\* confirming overall readiness despite unreviewed changes;

\* creating a new recommendation without revising the earlier one;

\* referring to an outdated project state;

\* or producing conflicting statements across the summary and final recommendation.



\## Future Comparison



After the run, I will compare the Phase 1 recommendation, proactive summary, and Phase 2 recommendation.



This comparison will show whether the explicit boundary and summary helped the agent track the requirement change and maintain a coherent current state.



