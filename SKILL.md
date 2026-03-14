---
name: code-review
description: Use this skill to audit code changes for compliance with project standards, strict typing, architecture rules, and security best practices.
version: 1.0.0
---

## Overview

This skill provides a systematic way to review code changes. It ensures that all contributions adhere to the strict rules defined in `AGENTS.md`, follow the NestJS + CQRS architectural patterns, and maintain high security and performance standards.

## Review Checklist

### 1. Type Safety (Strict)
*   **No `any`**: Ensure `any` is not used. Use `unknown` + type guards or precise interfaces.
*   **No `!` (Non-null assertions)**: Check for explicit null/undefined handling.
*   **Discriminated Unions**: Verify use of discriminated unions for state and error handling.
*   **Strict Imports**: Ensure `@/` path aliases are used for all project-internal imports. No `../` parent relative imports.

### 2. NestJS & Architecture
*   **Dependency Injection**: Ensure services are injected via constructors and not manually instantiated or accessed via globals.
*   **Modularization**: Check that logic is placed in the correct Module, Controller, or Service.
*   **CQRS Compliance**:
    *   **Record Layer**: Only handles write/state-modifying operations.
    *   **Read Layer**: Only handles query/data-retrieval operations.
*   **Named Exports**: Ensure no default exports are used.

### 3. Security & Reliability
*   **Subprocess Safety**: Check that `child_process.spawn` is used with argument arrays, never shell-interpolated strings.
*   **Isolation**: Verify that session workers cannot access each other's state or directories.
*   **Atomic Updates**: Ensure config changes are written atomically (write-to-temp + rename).
*   **Logging**: Confirm no secrets or raw user content are logged. Use the structured JSON logger.

### 4. Testing
*   **Meaningful Assertions**: Avoid shallow tests; ensure tests verify actual behavior and side effects. especially bussiness logic(ex: CQRS part)

### 5. error handling 
*   **Error Handling**: Ensure error handling is implemented correctly. especially when using external API or subprocess.
*   **Error tracing**: Are we using Rollbar to trace errors? 


## Review Output Format

Reviews should produce a categorized report:

*   🔴 **Must Fix**: Critical violations (e.g., use of `any`, shell interpolation, broken DI).
*   🟡 **Improvement**: Suggested optimizations or readability enhancements.
*   🔵 **Nitpick**: Minor stylistic comments.
*   ✅ **LGTM**: Section is approved.
