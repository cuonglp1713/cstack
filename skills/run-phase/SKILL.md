---
name: run-phase
description: Implement an authorized, defined phase or focused bug fix in a software repo, preserving local architecture and leaving a verified handoff. Use for implementation requests, not initial brainstorming or status-only questions.
---

# Implement one reviewable slice

1. Read repo instructions, `.cstack/CONTEXT.md`, active `.cstack/PLAN.md`/`PROGRESS.md` if the private kit is present, and relevant source, tests, contract, and feature-map row or detail. Otherwise use the repo's own task documents. Open a past phase report only when the task depends on it. Compare notes with Git status and current code; copied seed documents or missing records do not establish the application's state.
2. State the observable outcome, in/out scope, acceptance criteria, and likely files. A direct user request for a defined feature, fix, or slice is authorization to implement it, including when the kit has just been adopted and no phase has been recorded. Do not gate the work on inventorying unrelated features or reconstructing past phases. If a new product decision, incompatible contract change, or external rollout is needed, surface that decision while completing independent authorized work.
3. Follow the project's actual architecture and directory layout. For a FastAPI project without an established structure, prefer thin routers, typed schemas, domain services, DB/models, and separate worker entry points when needed. Repo-specific choices override global stack defaults.
4. Implement the smallest coherent change. Preserve unrelated edits. Add tests only when they prove behavior or protect a meaningful invariant. Use disposable infrastructure for migration/integration checks.
5. Verify the user-visible result and relevant side effect using `verify-backend` where applicable. Inspect the diff and record failures and skipped checks accurately.
6. Use `handoff-phase` after material work to record private results in `.cstack/docs/` when the kit is present and update relevant living indexes. Follow the repo's established documentation convention when the kit is absent. Record team-relevant behavior and decisions in shared project artifacts when required. Close the requested slice only from actual evidence; do not infer owner approval of another phase from a green test or merge.
