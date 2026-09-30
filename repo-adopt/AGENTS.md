# Project instructions

This template is for adopting the kit in a repository that already has code. Reconcile it with existing project instructions before use. The user's request, established contracts, and repository decisions take precedence over generic defaults.

## Session entry

1. Read existing repo instructions, then inspect Git status, relevant source, tests, contracts, and project docs for the requested task. Treat `PLAN.md` and `PROGRESS.md` as navigation aids; compare them with current code.
2. Identify the current task and its observable acceptance criteria. If the user has already requested a defined feature or fix, start that work without requiring a full repository inventory or a retrospective phase plan.
3. Read only the relevant `FEATURE_MAP.md` row, verification notes, and past reports when they exist. Mark anything not inspected as unknown rather than inferring its state.
4. Use `grill-feature` for consequential open decisions, `run-phase` for defined implementation, `verify-backend` for backend proof, and `handoff-phase` after material work.

## Existing project contract

- Record confirmed product, stack, architecture, and operational decisions here as they become relevant. Do not replace an existing choice with a global default.
- Follow the repository's established source, test, and documentation layout. Do not create `backend/`, `frontend/`, or `docker/` merely because the new-repo template uses them.
- Keep existing document names and conventions where they serve the same purpose. If adopting the root `PLAN.md`, `PROGRESS.md`, `VERIFY.md`, and `FEATURE_MAP.md`, merge with same-named files rather than overwriting them.
- Apply phase IDs only to work tracked from adoption onward, unless the project already has its own scheme. Do not reconstruct old phases or claim complete feature coverage.

## Documentation and verification

- `PLAN.md` describes the current requested or proposed slice. `PROGRESS.md` records current status and the next action. Neither file is a history of all prior development.
- `VERIFY.md` holds reusable commands and recent observed proof. Existing tests or CI configuration are discoverable evidence, not a claim that this agent ran them.
- `FEATURE_MAP.md` is a partial index of user journeys discovered while working. Record delivery state separately from verification evidence; leave uninspected areas out of the map.
- Store detailed reports and lasting decisions in the repository's established documentation location. If none exists, choose a small location only when the work warrants it. Preserve unique evidence before shortening an index.
- Verify the changed behavior with checks appropriate to the repo. Preserve unrelated edits and use disposable or identified external targets.
