# Routing and Tool Grant Map

Target Codebase: Art & Craft Marketplace

Workflow: Add Product Review Feature

This map defines how work is routed between roles and which MCP tools each role is allowed to use.

| Role | Receives from Orchestrator | Produces | Tools Granted | Tools Intentionally Withheld | Boundary Reason | Autonomy |
|---|---|---|---|---|---|---|
| Planner | Feature request, repository path, acceptance criteria | Numbered plan, file list, open questions | `mcp__coursetools__file_read`, `mcp__coursetools__codebase_search` | `file_write`, `shell`, `test_runner`, `task_tracker`, `web_search` | The Planner only plans. Withholding write and execution tools prevents accidental code changes. | High |
| Implementer | Approved plan and file list | Modified files and implementation summary | `mcp__coursetools__file_read`, `mcp__coursetools__file_write`, `mcp__coursetools__codebase_search` | `shell`, `test_runner`, `task_tracker`, `web_search` | The Implementer may change code but must not test its own work or update final status. | Medium |
| Reviewer | Requirements, modified files, implementation summary | PASS or NEEDS_CHANGES review report | `mcp__coursetools__file_read`, `mcp__coursetools__codebase_search` | `file_write`, `shell`, `test_runner`, `task_tracker`, `web_search` | The Reviewer must remain read-only so it cannot silently modify code while reviewing it. | High |
| Tester | Modified files and acceptance criteria | PASS or FAIL test report | `mcp__coursetools__file_read`, `mcp__coursetools__test_runner` | `file_write`, `codebase_search`, `shell`, `task_tracker`, `web_search` | The Tester verifies the implementation but cannot edit code to make a failing test pass. | Medium |
| Project Manager | Final run summary after human approval | Status update confirmation | `mcp__coursetools__task_tracker` | `file_read`, `file_write`, `codebase_search`, `shell`, `test_runner`, `web_search` | Ticket updates are isolated from coding roles and happen only after human approval. | Medium |

## Routing and Evaluation

1. The Orchestrator invokes the Planner first.
2. The Planner returns a plan and expected file list.
3. The Orchestrator evaluates the plan for completeness and scope.
4. The Implementer receives only an approved plan.
5. The Reviewer evaluates the implementation without modifying files.
6. If the Reviewer returns `NEEDS_CHANGES`, the Orchestrator routes the findings back to the Implementer.
7. If review passes, the Tester receives the modified files and acceptance criteria.
8. If tests fail, the Orchestrator routes the failure information back to the Implementer.
9. If review and tests pass, a human must approve the result.
10. Only after human approval may the Project Manager update the final ticket status.

## Important Tool Boundary

The Reviewer is intentionally denied `mcp__coursetools__file_write`.

This prevents the Reviewer from changing the same code it is responsible for independently evaluating. This boundary reduces the risk that review findings could be hidden by unauthorized edits.

## Alternative Considered

The Reviewer could have been granted `file_write` so it could immediately fix small issues. This was rejected because combining review and implementation responsibilities would weaken independent verification and make failures harder to diagnose.