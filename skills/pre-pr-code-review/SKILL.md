---
name: pre-pr-code-review
description: Reviews only user-specified changed files before opening a pull request, focusing on errors that could break the application, logical bugs, and incorrect patterns. Avoids refactors and style feedback unless necessary for correctness. Use when the user says “review staging note”, “pre PR review”, “before I open a PR”, or requests a focused PR-readiness check.
---

# Pre-PR Code Review (Focused, PR-Readiness)

## Scope rules (must follow)

- Review **only** the files the user lists (or explicitly pastes). Do not expand scope to other files unless the user asks.
- If the user says “staging note” or similar: assume the goal is **safe PR creation** (no app-breaking regressions).
- If an **auth** file is mentioned as “debug only”, you may still check for:
  - obvious runtime crashes / syntax errors
  - accidental secrets committed
  - anything that would break startup/imports
  - but otherwise **do not** suggest changes there.

## What to look for (priority order)

1. **App-breaking issues**
   - Type errors that would fail build/compile
   - Null/undefined crashes, unhandled promise rejections
   - Incorrect imports/exports, circular deps introduced by changes
   - API contract mismatches (request/response shape, required params)
   - Migration/schema changes that break runtime expectations
2. **Logical bugs**
   - Incorrect conditionals, off-by-one, wrong units/timezones
   - Race conditions, stale state, double submissions
   - Incorrect default values, inverted feature flags
3. **Incorrect or risky patterns (only if they matter)**
   - Security footguns (authz checks missing, injection risk, unsafe deserialization)
   - Data-loss risks (overwrites, destructive updates, missing transactions)
   - Observability gaps that hide failures (swallowed errors) when it affects correctness

## What NOT to do

- No refactoring suggestions if the code is already correct.
- No style/formatting opinions unless they directly cause a bug or build failure.
- Don’t request extra files beyond the listed ones unless absolutely required to validate a **breaking** issue.

## Output format (keep it short)

If there are issues, report them in this exact structure:

- **Breaking (must fix)**:
  - File: `path` — what will break + why + minimal fix suggestion
- **Bug / logic (should fix)**:
  - File: `path` — what’s wrong + concrete impact + minimal fix suggestion
- **Necessary improvement (only if needed)**:
  - File: `path` — improvement tied to correctness/safety

If you find **no issues that could break the application**, reply with exactly:

**Good to go.**

## Minimal review workflow

When the user provides a list of changed files:

1. Confirm you will review **only** those files.
2. Scan for build/runtime breakers first (imports, types, nullability, async).
3. Then scan for logic correctness and contract mismatches.
4. Provide either the issue list (using the required format) or “Good to go.”
