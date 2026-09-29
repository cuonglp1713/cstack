---
name: handoff-phase
description: Leave a concise cross-session record after a phase, bug fix, design decision, or verification changes in a repo. Use for material state changes, not routine status reads.
---

# Leave the next session a reliable starting point

1. Check current branch, Git status/HEAD, changed source, relevant tests, and any existing PLAN/PROGRESS/VERIFY files. Distinguish committed behavior from uncommitted work and ignored files.
2. In the owning component's `backend/docs/phases/P-XX.md` or `frontend/docs/phases/P-XX.md`, record each completed child ID, delivered behavior, changed code/commit, exact command and environment, observed result and side effect, limits, decisions, and remaining work. Update the report as children finish; finalize it when the parent phase closes. Follow the repo's own layout if it differs.
3. In `PROGRESS.md`, update the current status, blocker, and next allowed action. Keep one summary row and report link per parent phase; do not append the child history here. A test pass or merge does not imply owner approval of a new phase.
4. In `PLAN.md`, keep only the active slice. Preserve stable IDs and archive completed outcomes before replacing its content. In `VERIFY.md`, keep reusable commands and the latest relevant proof summary with a report link; put historical evidence in the phase report. Do not paste long logs or secrets.
5. Update affected `FEATURE_MAP.md` rows when user journeys or proof paths change. Keep it a short repo-specific index and link longer detail under the owning component's `docs/features/`. Put lasting architecture decisions in that component's `docs/adr/`; keep stable repo instructions in `AGENTS.md`.
6. Before shortening a root file, ensure unique decisions, results, and limitations survive in a report or ADR. End with a brief self-contained summary of changed behavior, proof, remaining uncertainty, and next action.
