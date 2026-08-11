# Routing and Tool Grant Map

Target Codebase: Art & Craft Marketplace

Workflow: Product Review Feature - Lessons Learned

Project ID: `proj-lessons`

This map defines how work is routed between roles and which MCP tools each role is allowed to use. Storage and retrieval access is granted only where required by the role's responsibility.

| Role | Responsibility | Tools Granted | Storage / Retrieval Access | Classification Ceiling | Tools Intentionally Withheld | Boundary Reason |
| --- | --- | --- | --- | --- | --- | --- |
| Planner | Create the implementation plan before code is changed | `mcp__coursetools__file_read`, `mcp__coursetools__codebase_search`, `mcp__retrieval__retrieve` | Retrieval only. Must retrieve permitted prior lessons before proposing the implementation approach. | `internal` | `file_write`, `shell`, `test_runner`, `task_tracker`, `web_search`, storage write operations | The Planner needs project knowledge to make an informed plan but does not need to modify code or persistent storage. |
| Implementer | Make the approved code change and record a new lesson learned | `mcp__coursetools__file_read`, `mcp__coursetools__file_write`, `mcp__coursetools__codebase_search`, `mcp__storage__write_entry` | May write exactly the project knowledge generated during implementation through the storage MCP server. | `internal` | `test_runner`, `task_tracker`, broad administrative operations | The Implementer must modify code and record a newly discovered lesson, but should not test its own work or update final project status. |
| Reviewer | Independently review the implementation | `mcp__coursetools__file_read`, `mcp__coursetools__codebase_search`, `mcp__retrieval__retrieve` | Retrieval only. Retrieves relevant prior lessons while evaluating the change. | `internal` | `file_write`, `shell`, `test_runner`, `task_tracker`, storage write operations | The Reviewer needs prior lessons for evidence-based review but must remain read-only so it cannot silently modify the code it evaluates. |
| Tester | Run the available tests and evaluate acceptance criteria | `mcp__coursetools__file_read`, `mcp__coursetools__test_runner` | No storage or retrieval access required for this workflow. | N/A | `file_write`, `codebase_search`, `shell`, `task_tracker`, storage write operations | The Tester only needs the implementation and test suite. Keeping its access narrow prevents test failures from being hidden through code edits. |
| Project Manager | Update final project status after successful verification and human approval | `mcp__coursetools__task_tracker` | No storage or retrieval access required. | N/A | `file_read`, `file_write`, `codebase_search`, `shell`, `test_runner`, storage and retrieval operations | The Project Manager only needs status-management capability and should not participate in implementation, review, or knowledge storage. |

## Workflow Routing

1. The Orchestrator sends the feature request, repository path, and acceptance criteria to the Planner.
2. The Planner retrieves permitted prior lessons from `proj-lessons` using `classification_ceiling = internal`.
3. The Planner creates a scoped implementation plan using the retrieved lessons and Target Codebase evidence.
4. The Orchestrator evaluates the plan before implementation begins.
5. The Implementer receives the approved plan and makes only the approved code changes.
6. After implementation, the Implementer records one new internal lesson through `mcp__storage__write_entry`.
7. The Reviewer retrieves relevant prior lessons from `proj-lessons` at an `internal` ceiling before evaluating the implementation.
8. The Reviewer returns `PASS` or `NEEDS_CHANGES` without modifying code.
9. If review passes, the Tester runs the test suite and returns `PASS` or `FAIL`.
10. If review or testing fails, findings are routed back to the Implementer.
11. After successful review and testing, human approval is required before final completion.
12. The Project Manager updates a ticket only when a real ticket identifier exists. No identifier is invented when one is unavailable.

## Classification Boundary

Retrieval-capable roles in this workflow operate with:

- `project_id = proj-lessons`
- `classification_ceiling = internal`

The corpus intentionally contains `lesson-sensitive-configuration.md`, which is classified as `confidential`.

During validation, retrieval calls made with an `internal` ceiling did **not** return this confidential document. This demonstrates that the classification boundary was enforced by the retrieval system rather than merely requested in agent instructions.

## Storage Boundary

The Implementer records new workflow discoveries through the storage MCP server rather than writing directly to `storage.db`.

The workflow verified that:

- the new lesson was written through `write_entry`;
- the entry could be read back through the storage MCP server;
- the entry remained available after the storage server was restarted;
- the storage audit log contained the corresponding write activity.

No workflow role directly accessed the storage database to create or modify stored knowledge.

## Reviewer Boundary

The Reviewer is intentionally granted retrieval access but denied file-write access.

This separation allows the Reviewer to use prior lessons as evidence while preserving independent review. During the live workflow, the Reviewer retrieved internal lessons and remained read-only throughout the evaluation.

## Least-Privilege Decision

Storage and retrieval capabilities are not granted uniformly across the team.

- The Planner receives retrieval because prior lessons affect planning.
- The Implementer receives storage write capability because implementation can generate new lessons.
- The Reviewer receives retrieval because prior lessons can inform verification.
- The Tester and Project Manager receive neither capability because their bounded responsibilities do not require them.

This keeps each role's authority limited to the operations necessary to complete its assigned responsibility.
