---
name: run-spec
description: Implement an authorized, bounded spec or focused bug fix in a software repo, preserving local architecture and leaving a verified handoff. Use for implementation requests, not initial brainstorming or status-only questions.
---

# Implement one bounded change

1. Read repo instructions, `.cstack/CONTEXT.md`, the active `.cstack/PLAN.md` and `.cstack/PROGRESS.md` if the private kit is present, and relevant source, tests, contracts, and feature-map detail. Read `spec.md`, `plan.md`, and `tasks.md` for an active spec. Otherwise use the repo's task documents. Open a completed spec only when the task depends on it. Compare notes with Git status and current code; copied templates or missing records do not establish application state.
2. State the observable outcome, in/out scope, acceptance criteria, and likely files. A direct user request for a defined feature or fix authorizes implementation, including when the kit has just been adopted and no spec exists yet. For substantial tracked work, create the spec record described in `.cstack/CONTEXT.md` once the scope is clear; a focused fix can proceed directly when no durable record is needed. Do not gate work on inventorying unrelated features or reconstructing old specs. Surface any new product decision, incompatible contract change, or external rollout while completing independent authorized work.
3. Follow the project's actual architecture and directory layout. For a FastAPI project without an established structure, prefer thin routers, typed schemas, domain services, DB/models, and separate worker entry points when needed. Repo-specific choices override global stack defaults.
4. Implement the smallest coherent change. Update actionable steps in `tasks.md` when a spec exists. Preserve unrelated edits. Add tests only when they prove behavior or protect a meaningful invariant. Use disposable infrastructure for migration/integration checks.
5. Verify the user-visible result and relevant side effect using `verify-backend` where applicable. Inspect the diff and record failures and skipped checks accurately.
6. Use `handoff-spec` after material work to record the implementation and observed results in the active `result.md` when the kit is present, and update the living indexes. Follow the repo's documentation convention when the kit is absent. Record team-relevant behavior and decisions in shared project artifacts when required. Mark a spec done only from evidence; do not infer owner approval for another spec from a green test or merge.
