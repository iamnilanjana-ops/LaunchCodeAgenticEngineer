# Run 003 — Context Management in a Long-Running Session

## Date

August 6, 2026

## Exercise

Module 2, Lesson 2, Exercise 2.2: Manage Context in a Long-Running Agent Session

## Task

Perform a multi-phase, read-only review of the Art & Craft Marketplace React project and revise the project recommendation after a requirement changes.

## Agent

Build Review Agent v1.1

## Workflow Phases

### Phase 1 — Initial Project Review

The agent performed a read-only project review.

It:

* checked Git status;
* ran the React production build;
* separated errors from warnings;
* reported bundle sizes;
* and produced an initial prioritized recommendation.

The build succeeded with no errors or warnings.

Reported bundle sizes:

* JavaScript: 76.36 kB gzipped
* CSS: 1.07 kB gzipped

The initial recommendation did not confirm overall project readiness because unreviewed changes were reported.

### Phase 2 — Revised Project Review

After Phase 1, I introduced an explicit context boundary and changed one requirement.

The agent was required to revisit the Phase 1 recommendation and produce a revised recommendation using the new priority rule.

## Requirement Change

### Original Priority

Phase 1 prioritized reviewing source changes, documentation/configuration changes, repository cleanup, and then optional maintenance warnings.

### New Requirement

Accessibility concerns must be prioritized above optional dependency or maintenance warnings.

The agent had to revise its earlier recommendation rather than continue using the original priority order.

## Explicit Context Boundary

The context boundary was placed after the Phase 1 recommendation and before Phase 2.

At the boundary, I stated that:

* Phase 1 was complete;
* Phase 2 was beginning;
* the read-only requirement remained active;
* the Git-safety guardrail remained active;
* the Git-status discrepancy must remain unresolved;
* and the Phase 1 recommendation had to be revisited.

This boundary separated the initial review from the revised review and made the requirement change explicit.

## Proactive Summary

After introducing the new requirement, I asked the agent to summarize the current session state before producing the final recommendation.

The summary preserved:

* the current goal;
* active requirements;
* the accessibility-priority change;
* Phase 1 findings;
* the Phase 1 recommendation;
* the Git-status discrepancy;
* unresolved questions;
* and the next planned action.

The summary correctly preserved the requirement change and did not silently resolve the conflicting Git-status evidence.

## Compaction

Compaction was not used.

The session remained manageable using the explicit context boundary and proactive summary. There was no evidence that the context window had become crowded enough to justify compaction.

## Context Drift / Misfire

The main misfire involved Git status.

Before starting the container session, host PowerShell reported one modified file:

`docs/module2-iteration-log.md`

During Phase 1, the agent reported 30 pre-existing modified files.

These observations conflicted.

Instead of restarting the session or silently choosing one result, I introduced the discrepancy at the context boundary and instructed the agent to preserve it as unresolved.

The agent successfully carried this unresolved issue through the proactive summary and final Phase 2 recommendation.

## Phase 2 Result

The revised priorities were:

1. Resolve the Git-status discrepancy.
2. Review accessibility-related aspects of modified UI files.
3. Review remaining documentation and configuration changes.
4. Treat the optional browserslist/caniuse-lite update as the lowest priority.

The agent did not claim that an accessibility defect existed without evidence.

It correctly changed the priority of accessibility review because of the new requirement.

The agent continued to avoid confirming overall project readiness.

## Rubric Scores

### Accuracy — 3/4

The agent accurately reported the successful build, absence of build errors and warnings, and bundle sizes.

However, the agent's report of 30 modified files conflicted with the host PowerShell baseline showing one modified file. Because the project-state evidence was inconsistent, I scored accuracy 3 instead of 4.

### Task Adherence — 4/4

The agent followed the read-only requirement and retained the Recommendation Guardrail.

After the requirement changed, it correctly prioritized accessibility review above optional maintenance work.

It also revisited the earlier recommendation rather than ignoring the requirement change.

### Coherence — 4/4

The proactive summary preserved the current goal, active requirements, changed priority, Phase 1 findings, and unresolved Git-status discrepancy.

The final recommendation was consistent with the proactive summary and clearly revised the Phase 1 priority order.

## Evidence

Specific evidence supporting the scores:

* Build completed successfully.
* Errors: none.
* Warnings: none.
* JavaScript bundle: 76.36 kB gzipped.
* CSS bundle: 1.07 kB gzipped.
* Host PowerShell showed one modified file before the managed session.
* Agent reported 30 modified files during Phase 1.
* Agent preserved this discrepancy as unresolved during the proactive summary.
* Accessibility review moved above optional maintenance work in Phase 2.
* Agent explicitly stated that it was not claiming an accessibility defect existed.
* Agent did not confirm overall project readiness.

## Context-Management Technique Evaluation

The explicit context boundary worked well because it clearly separated the old priority from the new requirement while preserving the requirements that remained active.

The proactive summary was especially useful because it forced the agent to restate the current requirement set and preserve the Git-status discrepancy before producing the final recommendation.

The techniques prevented the agent from reverting to the Phase 1 priority order during Phase 2.

## Future Improvement

In a future run, I would verify and record Git status from both the host and container at the beginning of the session.

This would create a shared baseline before the agent begins its analysis and reduce the chance that environment-specific project-state information becomes a source of confusion.

## Relevant Commit SHAs

* `af05d12` — Added Module 2 context pre-session plan.
* `84251e4` — Added Module 2 context-management technique plan.
* `bad5485` — Moved context-management plans into the Module 2 documentation directory.
* `49427a5` — Added Module 2 context-management session summary.

## Overall Result

The managed session successfully demonstrated a requirement change in a long-running agent session.

The agent experienced one project-state inconsistency but maintained the updated requirement after the explicit context boundary and proactive summary.

Overall rubric score for this managed run:

**Accuracy: 3/4**
**Task Adherence: 4/4**
**Coherence: 4/4**

**Total: 11/12**
## Persistent Memory Verification

### Run 001

* **Date:** August 7, 2026
* **Agent:** Claude Code
* **Workflow:** Build and verify persistent memory
* **Memory system state:** Persistent memory system created and committed. Fresh-session verification not yet completed.
* **Commit SHA:** `4404a1d`
* **Project Memory:** `.memory/project/decisions/decision-001.md`
* **Knowledge File:** `.memory/knowledge/coding-standards.md`
* **Reference Index:** `.memory/reference/MEMORY_INDEX.md`
* **Knowledge protection:** Read-only permission verified inside the container using a non-root user. The write attempt returned `Permission denied`.
- **Startup-memory check:** PASS. In a genuinely fresh session, Claude Code found Decision 001, the coding standards Knowledge File, and the reference index. It correctly distinguished changing Project Memory from stable Knowledge, identified the write policies, and did not modify any files.
- **Task-resumption check:** PASS. Claude Code correctly identified the active cross-session decision, followed the stored project standards, recognized that manually pasted notes and full transcript storage were rejected approaches, and proposed an appropriate next action without modifying files.
- **Observation:** The fresh-session test also identified a possible continuity-design gap between the older `docs/session-notes.md` instruction in `CLAUDE.md` and the newer structured `.memory/project/` system.
- **Verification result:** PASS — both required fresh-session checks passed.
## Run 003 - Stale Memory Failure Test

- **Agent name/version:** Claude Code
- **Failure mode tested:** Stale memory
- **Task used:** Review the current project memory, summarize the project state, and suggest what to work on next.
- **Initial memory state commit:** `f0bf981`

### Initial Observation

The agent correctly recognized that `decision-002.md` had an expired review date and conflicted with the current memory rules. It did not apply the stale decision as valid.

Verbatim excerpt:

> "I found one issue in decision-002: its Review by date is 2026-07-01, which has passed."
>
> "I'm surfacing that conflict now rather than acting on decision-002 as written."

### Remediation

The stale test entry was restored to the correct decision and its review date was updated.

- Restored decision commit: `c459dfb`

A stronger stale-memory policy was then added to `CLAUDE.md`. The new policy requires the agent to check the `Review by` date before acting, report expired entries, ask for human confirmation, and wait before using them.

- Policy remediation commit: `dc9f3b4`

### Rerun Result

On the verification run, the agent used the corrected `decision-002` and also noticed that other decision files did not yet have review dates.

Verbatim excerpt:

> "Always check the index before adding a new entry, to avoid duplicates/conflicts (decision-002)."
>
> "Suggested next step: add a Review by date to decision-003 and decision-004 for consistency with 001/002, so the stale-memory check applies uniformly across all four entries."

### Pass/Fail

**Pass:** The agent did not use stale information as current, correctly followed the restored decision, and applied the review-date policy during the verification run.

### Remaining Limitation

The stale-memory policy is an instruction-based soft guard. It still depends on the agent following `CLAUDE.md`. A production system could add a deterministic validation script or hook that checks required review-date metadata automatically.
## Module 2 Lab — Track 1: Strengthen Project Memory

### Run 1 — Memory Consistency Review

- **Date:** August 7, 2026
- **Track:** Track 1 — Work with Built-In Agents and Strengthen Project Memory
- **Agent:** Claude Code
- **Task:** Review the existing persistent-memory system for consistency, freshness, and maintainability gaps.
- **Observation:** Claude found that decision-003.md and decision-004.md were missing the `Review by` metadata required by the stale-memory policy. It also found that the canonical Project Memory index listed only Decision 001, even though Decisions 002–004 were active.
- **Revision:** Added `Review by: 2026-11-05` to Decisions 003 and 004 and updated `.memory/project/MEMORY_INDEX.md` so all four active decisions were discoverable.
- **Commit:** `f90a7e1`
- **Result:** The memory system became more consistent with the stale-memory policy and more discoverable for fresh sessions.

### Run 2 — Fresh-Session Verification

- **Date:** August 7, 2026
- **Agent:** Claude Code
- **Session type:** Fresh session started without `--continue` or `--resume`.
- **Task:** Follow `CLAUDE.md` startup instructions and report all active Project Memory decisions, their review dates, stale-memory behavior, and writable/read-only memory layers.
- **Observation:** Claude successfully discovered all four active decisions and correctly reported `Review by: 2026-11-05` for each. It correctly explained the stale-memory policy and memory-layer permissions.
- **New issue discovered:** Claude found two Project Memory index files: `.memory/project/MEMORY_INDEX.md` and `.memory/project/decisions/MEMORY_INDEX.md`. Because both represented the same decisions, they could drift out of sync.
- **Revision:** Removed the unused duplicate `decisions/MEMORY_INDEX.md` and added a Canonical Index rule to `.memory/project/MEMORY_INDEX.md`.
- **Commit:** `9de1f1d`
- **Result:** PASS. Fresh-session memory retrieval worked, but the run exposed a maintainability risk that led to another improvement.

### Run 3 — Final Fresh-Session Verification

- **Date:** August 7, 2026
- **Agent:** Claude Code
- **Session type:** Fresh session started without `--continue` or `--resume`.
- **Task:** Verify the memory system after consolidating the Project Memory index.
- **Observation:** Claude confirmed that `.memory/project/MEMORY_INDEX.md` is the single canonical Project Memory index and that no duplicate Project Memory index remains.
- **Verification:** Claude discovered all four active decisions from the canonical startup path and reported `Review by: 2026-11-05` for each.
- **Result:** PASS. The startup process was complete and internally consistent, with no active problem preventing a future fresh session from using persistent memory correctly.
- **Remaining limitation:** Claude identified a future cleanup opportunity because `docs/session-notes.md` and structured Project Memory both provide continuity mechanisms. It also noted that read-only knowledge protection currently relies partly on instructions and that some memory files have formatting inconsistencies.
- **Next improvement:** Clarify the role of `docs/session-notes.md` versus structured Project Memory so future sessions have one clear continuity workflow.