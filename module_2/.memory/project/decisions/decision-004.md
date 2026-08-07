# Decision 004: Store Evolving Decisions in Project Memory

- **Date:** 2026-08-07
- **Status:** Active
- **Scope:** Project
- **Type:** Memory architecture decision

## Decision
Evolving project decisions and context that future sessions cannot reliably infer from the repository will be stored in `.memory/project/decisions/`. Stable reusable guidance remains in the knowledge layer, while reference material remains in the reference layer.

## Rationale
Code can show what was implemented, but it does not always explain why a choice was made, which alternatives were rejected, or which rule a future agent should continue following. Recording those decisions provides useful cross-session context without saving full conversation transcripts.

## Alternatives Rejected
- Rely only on repository code and Git history.
- Save full session transcripts as persistent memory.
- Put changing project decisions in the stable knowledge layer.

These approaches were rejected because they either lose important reasoning, overload future sessions with unnecessary context, or mix changing information with stable knowledge.

## Future Guidance
Add a project decision only when it is useful to future work and cannot be reliably inferred from the repository alone. Review entries when project decisions change so stale guidance does not remain active.
