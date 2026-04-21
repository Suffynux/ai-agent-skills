---
name: ai-pr-viewer
description: AI-powered Pull Request (PR) reviewer for all AI models, offering two modes: "PR Review and Fix" for comprehensive review and automated fixes, and "PR Review (major issues only)" for critical production-breaking issues.
---

# AI PR Viewer Skill

## Overview

This skill enables Gemini CLI to perform comprehensive Pull Request reviews with two distinct modes tailored to different levels of scrutiny and intervention. It leverages AI models to analyze code, identify potential issues, and, in one mode, propose and apply fixes.

## Modes of Operation

### Mode 1: PR Review and Fix (Comprehensive Review)

**Description:** In this mode, the AI PR Viewer performs a thorough analysis of the entire Pull Request. It identifies a wide range of issues, including but not limited to:
-   **Code Quality:** Adherence to coding standards, style guides, and best practices.
-   **Bugs and Errors:** Potential logical errors, off-by-one errors, unhandled exceptions, and other functional defects.
-   **Security Vulnerabilities:** Common vulnerabilities like injection flaws, improper authentication/authorization, insecure deserialization, etc.
-   **Performance Bottlenecks:** Inefficient algorithms, excessive resource consumption, and potential scaling issues.
-   **Maintainability:** Code complexity, readability, and ease of future modifications.
-   **Test Coverage:** Adequacy of unit, integration, and end-to-end tests.
-   **Documentation:** Clarity and completeness of inline comments, docstrings, and external documentation updates.

**Workflow:**
1.  **Analyze PR:** Read the PR description, changed files, and existing code context.
2.  **Identify Issues:** Systematically scan for all types of issues described above.
3.  **Propose Fixes:** For each identified issue, provide a clear explanation, its impact, and suggest concrete code changes or alternative approaches.
4.  **Apply Fixes (if confirmed):** If the user approves, automatically apply the proposed fixes using `replace` or `write_file` tools.
5.  **Re-verify:** After applying fixes, re-run relevant tests or checks to ensure the issue is resolved and no new regressions are introduced.

### Mode 2: PR Review (Major Issues Only)

**Description:** This mode focuses strictly on critical issues that could lead to immediate production failures, data corruption, security breaches, or significant performance degradation. It prioritizes stability and operational integrity above all else.

**Workflow:**
1.  **Analyze PR:** Read the PR description, changed files, and existing code context.
2.  **Identify Critical Issues:** Focus on:
    -   **Production-breaking Bugs:** Issues that would cause the application to crash, become unresponsive, or render core functionalities unusable in a production environment.
    -   **Severe Security Vulnerabilities:** Critical flaws (e.g., RCE, SQLi, XSS, authentication bypass) that pose an immediate and high risk to the system or user data.
    -   **Architectural Regressions:** Changes that fundamentally violate established architectural principles or introduce unmanageable technical debt that impacts scalability or reliability.
    -   **Resource Exhaustion:** Changes that could lead to uncontrolled resource consumption (CPU, memory, disk I/O, network) and system outages.
3.  **Report Major Issues:** For each critical issue, provide a concise explanation of the problem, its potential impact on production, and recommendations for immediate resolution. This mode does NOT propose or apply fixes automatically; it only highlights critical problems for human intervention.

## Usage Guidelines

-   When initiating a PR review, specify which mode to use.
-   Provide the PR context (e.g., link to the PR, or list of changed files and their contents).
-   Be prepared to confirm or refine proposed fixes in "PR Review and Fix" mode.

## Resources

This skill does not include specific scripts, references, or assets beyond its core instructions. It leverages Gemini CLI's inherent capabilities and general-purpose tools to perform code analysis and modifications.
