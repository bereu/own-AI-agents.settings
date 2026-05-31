```markdown
# Code Review: Session Worker Refactor

## Summary
Audit of the move from raw `child_process` to the new `SessionRunner` service in the `SessionsModule`.

## Review Results

### 1. Type Safety
- 🔴 **Must Fix**: `src/modules/sessions/session-runner.ts:42` — Use of `any` in `onProcessOutput(data: any)`. Change to `Buffer` or `string` and add type guard.
- ✅ **LGTM**: Excellent use of discriminated unions for `SessionEvent` types.

### 2. Architecture
- 🔴 **Must Fix**: `src/modules/sessions/sessions.controller.ts:15` — `new SessionRunner()` detected. Inject `SessionRunner` via the constructor instead.
- 🟡 **Improvement**: Consider moving the `afplay` logic to a dedicated `NotifyService` within a `SharedModule`.

### 3. Imports
- 🔴 **Must Fix**: `src/modules/sessions/session-runner.ts:5` — Relative import `../../shared/types` detected. Replace with `@/shared/types`.

### 4. Security
- ✅ **LGTM**: Verified that `claude` CLI is invoked with an argument array.
- ✅ **LGTM**: Structured logging implemented correctly without secret leakage.

### 5. Testing
- 🟡 **Improvement**: Add an integration test in `tests/integration/sessions/` to verify the runner handles process crashes during output streaming.

## Verdict
**Status**: 🔴 Changes Requested. Please address the `any` usage, dependency injection violation, and relative imports.
```
