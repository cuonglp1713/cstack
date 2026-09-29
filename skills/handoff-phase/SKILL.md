---
name: personal-handoff-phase
description: Leave a concise cross-session record after a phase, bug fix, design decision, or verification changes in a personal repo. Use for material state changes, not routine status reads.
---

# Leave the next session a reliable starting point

1. Check current branch, Git status/HEAD, changed source, relevant tests, and any existing PLAN/PROGRESS/VERIFY files. Distinguish committed behavior from uncommitted work and ignored files.
2. In `PROGRESS.md`, record the phase ID, state transition, decision, observed result, blocker, and next allowed action. A test pass or merge does not imply owner approval of a new phase.
3. In `PLAN.md`, revise scope and acceptance criteria only when decisions changed. Keep one active slice and preserve stable child IDs for audit.
4. In `VERIFY.md`, record exact command and environment, pass/fail/skip, observed side effect, and limits. Do not paste long logs or secrets.
5. Update only affected rows of `FEATURE_MAP.md` when user entry points or verification paths changed. Keep stable repo instructions in `AGENTS.md`; do not move transient status there.
6. End with a brief self-contained summary of changed behavior, proof, remaining uncertainty, and next action.
