# AGENTS.md - The Sovereign Constitution

This document is the **Single Source of Truth (SSoT)** for all AI agents. It defines high-level governance and the core behavioral logic of the autonomous development harness.

## 🏛 1. Strategic Context & Architecture
- **Tech Stack:** Java 25 (OpenJDK), Spring Boot 4.0.3, Gradle (Multi-module).
- **Database:** Oracle (Prod: ATP / Local: XE via Docker `gvenzl/oracle-xe`)
- **Architecture:** Domain-Driven Design (DDD) with `module-core`, `module-api`, and `module-batch`.
- **Standards:** Lombok, JUnit 5, Clean Code, SOLID.

## 🛡 2. Governance & Security
- **Security:** Follow `.gemini/skills/security_audit.md`. Zero-secret policy.
- **Harness Integrity:** Modifications to `.gemini/` or `AGENTS.md` require user confirmation.
- **DevOps:** Infrastructure and deployment follow `.gemini/skills/devops_pipeline_generator.md`.

## 📊 3. Agile Workflow (Extreme Granularity)
All tasking MUST adhere to the **Extreme Granularity** principle to minimize code changes and maximize context autonomy.
- **Reference:** See `.gemini/skills/scrum_master_planning.md` for issue templates and decomposition rules.
- **Goal:** One Task = One Functional Change/Bug Fix (50-100 LOC).
- **Title Formats:**
  - Epic: `[Epic] Strategic Objective Name`
  - Feature: `[Feature] Deliverable Unit Name`
  - Task: `[Task] Specific Atomic Work Name`

## 🚀 4. Autonomous Development Workflow (11 Steps)
1. **Receive Issue**: Issue number or objective from user.
2. **Pre-Analysis & Fetch**: Use `github_operator` to fetch the issue (and parent context).
3. **Understand & Plan**: Use `scrum_master_planning` to break down tasks if necessary.
4. **Environment Setup (Isolation)**: Use `workspace_manager` to create a `feature/issue-{{no}}` branch and an isolated `../worktree-{{no}}` environment. **[Mandatory Isolation Point]**
5. **Root Cause (RCA)**: Within the worktree, use `code_explorer` for deep analysis. **[Regression Point]**
6. **Solution Plan**: Formulate a JSON Action Plan following senior standards.
7. **Implementation**: Use `code_writer` to apply logic and unit tests inside the worktree.
8. **Verification**: Use `build_validator` for local test execution (`./gradlew test`).
9. **Local Verdict**: If failure, return to [Step 5] (GOTO 5).
10. **Reflect/Push & PR**: Commit changes to the feature branch, push to origin, and use `github_operator` to create a Pull Request. **[FINAL STEP]**
11. **STOP & Handover**: After PR creation, you MUST stop all autonomous actions. Do NOT merge the PR, do NOT push to `master`, and do NOT close the issue manually. Wait for user review and CI feedback.

## 🛡 5. Branch Safety & Governance
- **Direct Push Prohibition**: Direct pushes to `master` or `main` are STRICTLY PROHIBITED. All changes must go through a Pull Request.
- **Stop Condition**: An agent's task execution turn ends immediately after the `gh pr create` command.
- **Cleanup Policy**: `workspace_manager.cleanup()` should only be invoked after the PR is successfully merged and the user issues a explicit cleanup directive.

## 👥 5. Sub-Agent Role Definitions
- **Planner (Architect)**: Analysis, design, and task decomposition (`github_operator`, `code_explorer`).
- **Executor (Engineer)**: Implementation and isolated environment management (`workspace_manager`, `code_writer`).
- **Verifier (QA Lead)**: Validation and regression logic (`build_validator`, `github_operator`).

---
*Self-Evolution: Refer to `.gemini/skills/self_evolution.md` for workflow improvements.*
