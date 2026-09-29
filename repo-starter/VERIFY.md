# Verification guide and evidence

No application exists yet, so no check is marked passed. Replace the first section with real commands after the first runnable slice. Use `FEATURE_MAP.md` to find the user-facing path to exercise.

## Verification approach

1. Name the behavior and the environment: isolated test, disposable integration, dev live, or staging.
2. Run the smallest check that demonstrates the changed behavior. Observe input/action, output, and any important persisted or asynchronous side effect.
3. Run broader checks for a concrete cross-boundary risk or project gate. Keep skipped and blocked checks explicit.
4. Review the diff and record exact commands/results. Never substitute a fake test for live acceptance.

## Commands

- Build/start: not established yet.
- Focused test: not established yet.
- Full test/quality gate: not established yet.
- External acceptance: not established yet; use an explicitly named target and safe test data when added.

## Evidence entry format

```text
Phase and behavior:
Date and branch/commit:
Environment:
Action and exact command:
Observed result and side effect:
Pass / fail / skipped:
Limitation or follow-up:
```
