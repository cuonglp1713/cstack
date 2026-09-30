# Verification guide

No application exists yet, so no check is marked passed. Fill in commands after the first runnable change. Use `.cstack/FEATURE_MAP.md` to find the user-facing path to exercise.

## Verification approach

1. Name the behavior and environment: isolated test, disposable integration, dev live, or staging.
2. Run the smallest check that demonstrates the changed behavior. Observe input/action, output, and any important persisted or asynchronous side effect.
3. Run broader checks for a concrete cross-boundary risk or project gate. Keep skipped and blocked checks explicit.
4. Review the diff and record exact commands/results. Never substitute a fake test for live acceptance.

## Reusable commands

- Build/start: not established yet.
- Focused test: not established yet.
- Full test/quality gate: not established yet.
- External acceptance: not established yet; use a named target and safe test data when added.

## Latest relevant proof

- **Spec or focused fix:** none yet.
- **Result:** not run.
- **Detailed evidence:** no spec result yet.

Keep only the current or latest relevant proof summary here. When a spec exists, record date, branch/commit, environment, exact command/action, observed result and side effect, pass/fail/skip, and limitation in its `result.md`; link it above. Do not paste large logs or secrets.
