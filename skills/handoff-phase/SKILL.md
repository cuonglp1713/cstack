---
name: handoff-phase
description: Leave a concise cross-session record after a phase, bug fix, design decision, or verification changes in a repo. Use for material state changes, not routine status reads.
---

# Leave the next session a reliable starting point

1. Check current branch, Git status/HEAD, changed source, relevant tests, and any existing PLAN/PROGRESS/VERIFY files. Distinguish committed behavior from uncommitted work and ignored files. When adopting an existing repo, do not treat empty kit templates as a history of the product.
2. Record completed work, changed code/commit, exact command and environment, observed result and side effect, limits, decisions, and remaining work in the repo's established report location. If none exists, use concise current-work notes and choose a detailed report location only when warranted. Use the owning component's `backend/docs/phases/P-XX.md` or `frontend/docs/phases/P-XX.md` when the new-repo starter layout applies. Do not backfill reports or phase IDs for old features merely to adopt the kit.
3. In `PROGRESS.md` if present, update the current status, blocker, and next allowed action. Keep a short index of work tracked by the kit; do not append a full event log or imply full coverage of an existing repo. A test pass or merge does not imply owner approval of a new phase.
4. In `PLAN.md` if present, keep only the active slice. Preserve stable IDs and archive completed outcomes before replacing its content. In `VERIFY.md` if present, keep reusable commands and the latest relevant proof summary; put historical evidence in the appropriate report when the repo uses one. Do not paste long logs or secrets.
5. Update affected `FEATURE_MAP.md` rows when user journeys or proof paths change. Keep it a short repo-specific index, leave uninspected journeys unmapped, and link longer detail in the repo's established docs location. Put lasting architecture decisions with existing project decisions or ADRs; keep stable repo instructions in `AGENTS.md`.
6. Before shortening a root file, ensure unique decisions, results, and limitations survive in a report or ADR. End with a brief self-contained summary of changed behavior, proof, remaining uncertainty, and next action.
