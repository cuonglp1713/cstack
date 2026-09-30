# Current plan

This is a private seed for a new repository. Keep only the current proposed or authorized slice here. Before replacing a completed slice, put its outcome and evidence in `.cstack/docs/phases/P-XX.md`, then leave a short pointer in `.cstack/PROGRESS.md`.

## P-00.1 — Define the first vertical slice

- **Status:** proposed; the product idea has not yet been provided.
- **User outcome:** not decided yet.
- **In scope:** clarify the target user, core problem, first observable behavior, and necessary technical constraints.
- **Out of scope:** features, services, and integrations not needed for the first slice.
- **Decisions to resolve:** what the user can do, what data persists, what failure looks like, and how success will be verified.
- **Acceptance criteria:** a small implementation slice can be stated with concrete input, output, and proof; any remaining unknown has an owner or a small probe.
- **Implementation authorization:** a direct user request to build a defined slice authorizes it. Otherwise this section is planning state only.

## Slice format for later phases

```text
ID and title:
Status: proposed | authorized | implementing | awaiting_review | approved | blocked
User outcome:
In scope / out of scope:
Relevant contract or ADR:
Decisions and open questions:
Observable acceptance criteria:
Verification plan:
Data, rollout, or migration risk:
```

Use a child ID, for example `P-01.2`, when one independently reviewable outcome needs its own decision and evidence. Avoid splitting trivial edits merely to create phases.
