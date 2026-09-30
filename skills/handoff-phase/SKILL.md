---
name: handoff-phase
description: Leave a concise cross-session record after a phase, bug fix, design decision, or verification changes in a repo. Use for material state changes, not routine status reads.
---

# Leave the next session a reliable starting point

1. Check current branch, Git status/HEAD, changed source, relevant tests, and `.cstack/PLAN.md`, `.cstack/PROGRESS.md`, and `.cstack/VERIFY.md` when the private kit is present. Otherwise use the repo's own handoff documents. Distinguish committed behavior from uncommitted work and ignored files. When adopting an existing repo, do not treat empty kit templates as a history of the product.
2. Record completed work, changed code/commit, exact command and environment, observed result and side effect, limits, decisions, and remaining work in `.cstack/docs/phases/P-XX.md` when the private kit is present and a detailed report is warranted. For smaller work, keep concise private results in `.cstack/PROGRESS.md` and `.cstack/VERIFY.md`. If the kit is absent, use the repo's established report location. Do not backfill reports or phase IDs for old features merely to adopt the kit.
3. In `.cstack/PROGRESS.md` if present, update the current status, blocker, and next allowed action. Keep a short index of work tracked by the kit; do not append a full event log or imply full coverage of an existing repo. When the kit is absent, follow the repo's progress convention. A test pass or merge does not imply owner approval of a new phase.
4. In `.cstack/PLAN.md` if present, keep only the active slice. Preserve stable IDs and archive completed outcomes before replacing its content. In `.cstack/VERIFY.md` if present, keep reusable commands and the latest relevant proof summary; put historical evidence in the appropriate report when the repo uses one. When the kit is absent, follow the repo's plan and verification conventions. Do not paste long logs or secrets.
5. Update affected `.cstack/FEATURE_MAP.md` rows when user journeys or proof paths change. Keep it a short repo-specific index, leave uninspected journeys unmapped, and link longer personal detail in `.cstack/docs/features/`. Put personal decision notes in `.cstack/docs/adr/`; when the kit is absent, follow the repo's equivalent conventions. Record team-relevant decisions and instructions in shared project artifacts when required.
6. Before shortening a living file, ensure unique decisions, results, and limitations survive in a report or decision note. End with a brief self-contained summary of changed behavior, proof, remaining uncertainty, and next action.
