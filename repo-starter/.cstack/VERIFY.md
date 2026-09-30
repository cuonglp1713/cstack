# Verification guide

No application exists yet, so no check is marked passed. Replace command placeholders after the first runnable slice. Use `.cstack/FEATURE_MAP.md` to find the user-facing path to exercise.

## Verification approach

1. Name the behavior and the environment: isolated test, disposable integration, dev live, or staging.
2. Run the smallest check that demonstrates the changed behavior. Observe input/action, output, and any important persisted or asynchronous side effect.
3. Run broader checks for a concrete cross-boundary risk or project gate. Keep skipped and blocked checks explicit.
4. Review the diff and record exact commands/results. Never substitute a fake test for live acceptance.

## Reusable commands

- Build/start: not established yet.
- Focused test: not established yet.
- Full test/quality gate: not established yet.
- External acceptance: not established yet; use an explicitly named target and safe test data when added.

## Latest relevant proof

- **Slice:** `P-00.1`.
- **Result:** not run; no application exists.
- **Detailed evidence:** no phase report yet.

Keep only the current or latest relevant proof summary here. In `.cstack/docs/phases/P-XX.md`, record the child ID, date and branch/commit, environment, exact command/action, observed result and side effect, pass/fail/skip, and limitation. Link that report above. Do not paste large logs or secrets.
