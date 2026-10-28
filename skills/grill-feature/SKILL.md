---
name: grill-feature
description: Turn an ambiguous product or engineering idea into clear decisions and a bounded implementable spec. Use for vague features, architecture choices, or new projects; skip when scope and acceptance criteria are already clear.
---

# Clarify the idea

1. Read the user's idea, repository instructions, relevant `.cstack/CONTEXT.md`, `.cstack/PLAN.md`, and `.cstack/PROGRESS.md` when present, code, tests, contracts, or product notes. Use PROGRESS to locate current work and PLAN to understand its intended scope and approach; otherwise follow the repo's planning convention. In an existing repo, inspect current behavior and work in progress around the requested change; do not require a full repository inventory. State the outcome you think they want. Do not ask questions already answered by these sources.
2. Ask consequential questions in small rounds. Cover users and success, boundaries, key data, failure behavior, security, deployment constraints, and observable acceptance only where each can change the next decision. Later questions should build on earlier answers.
3. Mark each point as decided, inferred, or unknown. If a choice cannot be settled by discussion, propose the smallest prototype or research check that would settle it; avoid endless hypothetical questions.
4. End when one bounded change can be implemented without hidden assumptions. Summarize decisions, remaining uncertainty, and acceptance criteria. The user owns product scope.
5. When asked to make the plan durable, follow the project's spec location and filenames; otherwise use `.cstack/specs/<id>-<slug>/` for private kit records. Derive the slug from actual work; do not create specs before scope is known or backfill old features. Record outcome, boundaries, decisions, and acceptance in the spec (`spec.md` or the existing `README.md`). A spec may have several phases/slices with stable IDs and their own acceptance; identify the next slice without treating the roadmap as authorization. Record approach and steps in `plan.md` or existing phase plans; child/task tables suffice without a separate `tasks.md`. In `.cstack/PLAN.md` when present, keep the agreed scope, acceptance, approach, phase dependencies, verification plan, and detail links. In `.cstack/PROGRESS.md`, record the current or proposed work, active or waiting slice, status, and next action. Put lasting confirmed project decisions in CONTEXT; do not create another progress index under specs.
6. If `.cstack/FEATURE_MAP.md` exists, update only relevant journeys. Mark a new unbuilt journey as planned when useful; inspect existing code before recording an implemented or in-progress path, and do not claim verification without observed proof. Leave uninspected features unmapped.

This is an inquiry workflow inspired by Matt Pocock's `grill-me`, adapted for codebases and spec planning. Do not turn it into a fixed questionnaire.
