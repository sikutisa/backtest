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

## 🚀 4. Autonomous Development Workflow (10 Steps)
1. **Receive Issue**: Issue number or objective from user.
2. **Pre-Analysis & Fetch**: Use `github_operator` (fetch parent if sub-task).
3. **Understand**: Analyze requirements and intent.
4. **Root Cause (RCA)**: Use `code_explorer` for deep analysis. **[Regression Point]**
5. **Solution Plan**: High-fidelity JSON Action Plan following senior standards.
6. **Implementation**: `workspace_manager` (isolation) + `code_writer` (logic & tests).
7. **Verification**: `build_validator` for local test execution.
8. **Local Verdict**: If failure, return to [Step 4] with logs (GOTO 4).
9. **Reflect/Push**: Commit and push to remote.
10. **CI Monitor**: Use `github_operator`. If CI fails, return to [Step 4] (GOTO 4).

## 👥 5. Sub-Agent Role Definitions
- **Planner (Architect)**: Analysis, design, and task decomposition (`github_operator`, `code_explorer`).
- **Executor (Engineer)**: Implementation and isolated environment management (`workspace_manager`, `code_writer`).
- **Verifier (QA Lead)**: Validation and regression logic (`build_validator`, `github_operator`).

---
*Self-Evolution: Refer to `.gemini/skills/self_evolution.md` for workflow improvements.*
