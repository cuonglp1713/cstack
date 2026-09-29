---
name: personal-run-phase
description: Implement an authorized, defined phase or focused bug fix in a personal software repo, preserving local architecture and leaving a verified handoff. Use for implementation requests, not initial brainstorming or status-only questions.
---

# Implement one reviewable slice

1. Read repo `AGENTS.md`, active `PLAN.md`/`PROGRESS.md` if present, and relevant source, tests, contract, and feature-map row. Compare notes with Git status and current code; do not trust a stale snapshot over source.
2. State the observable outcome, in/out scope, acceptance criteria, and likely files. A direct user request for a defined slice is authorization to implement it. If a new product decision, incompatible contract change, or external rollout is needed, surface that decision while completing independent authorized work.
3. Follow the project's actual architecture. For a FastAPI project without an established structure, prefer thin routers, typed schemas, domain services, DB/models, and separate worker entry points when needed. Repo-specific choices override personal stack defaults.
4. Implement the smallest coherent change. Preserve unrelated edits. Add tests only when they prove behavior or protect a meaningful invariant. Use disposable infrastructure for migration/integration checks.
5. Verify the user-visible result and relevant side effect using `personal-verify-backend` where applicable. Inspect the diff and record failures and skipped checks accurately.
6. Use `personal-handoff-phase` after material work. Close the requested slice only from actual evidence; do not infer owner approval of another phase from a green test or merge.
