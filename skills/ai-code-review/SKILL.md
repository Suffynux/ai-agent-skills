---
name: ai-code-review
description: Comprehensive AI-powered code review capabilities, including detailed analysis, bug and security vulnerability detection, best practices recommendations, and automated fix suggestions. This skill integrates with the 'ai-pr-viewer' for flexible pull request review modes.
---

# AI Code Review Skill

This skill provides comprehensive code review capabilities powered by AI agents, offering in-depth analysis and actionable insights to improve code quality, security, and maintainability.

## Key Features

-   **Deep Code Analysis:** Thorough examination of code for potential issues, anti-patterns, and deviations from best practices.
-   **Bug and Security Vulnerability Detection:** Identification of common bugs, logical errors, and security vulnerabilities (e.g., injection flaws, insecure configurations).
-   **Best Practices Recommendations:** Suggestions for adhering to coding standards, style guides, and idiomatic language usage.
-   **Performance Optimization Suggestions:** Identification of inefficient code segments and recommendations for performance improvements.
-   **Test Coverage Analysis:** Assessment of existing test suites and suggestions for improving test coverage.
-   **Maintainability Insights:** Evaluation of code complexity, readability, and suggestions for improving long-term maintainability.

## Integrated with AI PR Viewer

This skill is fully integrated with the `ai-pr-viewer` skill, which offers two distinct modes for conducting pull request reviews:

### Mode 1: PR Review and Fix (Comprehensive Review)

Performs an exhaustive review, identifying a wide range of issues across code quality, bugs, security, performance, maintainability, test coverage, and documentation. It also proposes concrete fixes and can automatically apply them upon user confirmation.

### Mode 2: PR Review (Major Issues Only)

Focuses exclusively on critical issues that could lead to immediate production failures, severe security breaches, or significant performance degradation. This mode highlights critical problems for human intervention without automatically proposing or applying fixes.

## Usage

To leverage the AI Code Review capabilities, specify your desired review mode (e.g., "PR Review and Fix" or "PR Review (Major Issues Only)") and provide the context of the code or pull request to be reviewed.

---

*Thank you for your interest in AI Agent Skills.*
