# Personal project context

This private template is for adopting the kit in a repository that already has code. Reconcile it with existing project instructions before use. The user's request, established contracts, and repository decisions take precedence over personal defaults. The global `~/.codex/AGENTS.md` points the agent to this file; Codex does not load it automatically from the repository root.

## Session entry

1. Read existing repo instructions, then inspect Git status, relevant source, tests, contracts, and project docs for the requested task. Treat `.cstack/PLAN.md` and `.cstack/PROGRESS.md` as navigation aids; compare them with current code.
2. Identify the current task and its observable acceptance criteria. If the user has already requested a defined feature or fix, start that work without requiring a full repository inventory or a retrospective phase plan.
3. Read only the relevant `.cstack/FEATURE_MAP.md` row, verification notes, and past reports when they exist. Mark anything not inspected as unknown rather than inferring its state.
4. Use `grill-feature` for consequential open decisions, `run-phase` for defined implementation, `verify-backend` for backend proof, and `handoff-phase` after material work.

## Existing project contract

- Record confirmed product, stack, architecture, and operational decisions here as personal context when relevant. Keep team-relevant decisions in the project's shared artifacts. Do not replace an existing choice with a global default.
- Follow the repository's established source, test, and documentation layout. Do not create `backend/`, `frontend/`, or `docker/` merely because the new-repo template uses them.
- Keep personal kit notes inside `.cstack/`. Leave existing root `AGENTS.md`, plans, verification guides, and other team documents intact; consult them as project evidence.
- Apply phase IDs only to work tracked from adoption onward, unless the project already has its own scheme. Do not reconstruct old phases or claim complete feature coverage.

## Documentation and verification

- `.cstack/PLAN.md` describes the current requested or proposed slice. `.cstack/PROGRESS.md` records current status and the next action. Neither file is a history of all prior development.
- `.cstack/VERIFY.md` holds reusable commands and recent observed proof. Existing tests or CI configuration are discoverable evidence, not a claim that this agent ran them.
- `.cstack/FEATURE_MAP.md` is a partial index of user journeys discovered while working. Record delivery state separately from verification evidence; leave uninspected areas out of the map.
- Store detailed personal reports and decision notes in `.cstack/docs/` when warranted. Preserve unique evidence before shortening an index; use the repository's established docs for information the team needs to share.
- Verify the changed behavior with checks appropriate to the repo. Preserve unrelated edits and use disposable or identified external targets.
