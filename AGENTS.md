# AGENTS.md - The Sovereign Constitution of Autonomous Agents

This document is the **Single Source of Truth (SSoT)** for all AI agents operating within this workspace. It defines the technical boundaries, behavioral ethics, and the governance protocol for autonomous development.

## 🏛 1. Strategic Context Boundaries

### Core Tech Stack
- **Language:** Java 25 (OpenJDK)
- **Framework:** Spring Boot 4.0.3
- **Build Tool:** Gradle (Multi-module architecture)
- **Database:** PostgreSQL (with Flyway for migrations)
- **Architecture:** Domain-Driven Design (DDD) with clean separation of concerns:
    - `module-core`: Domain entities and core business logic.
    - `module-api`: RESTful APIs and external integrations.
    - `module-batch`: Data crawling and bulk ingestion.

### Performance Heuristics
- **Efficiency:** Minimize context usage by prioritizing surgical edits and targeted research.
- **Reliability:** Always verify changes with `./gradlew build` before concluding a task.
- **Cleanliness:** Adhere strictly to project-specific coding standards (Lombok, JUnit 5).

## 🛡 2. Security & Compliance
All security operations MUST follow the protocols defined in `.gemini/skills/security_audit.md`.
- **No-Secret Policy:** Zero tolerance for credential leaks.
- **Tool Restriction:** All `run_shell_command` calls must adhere to the allow-list in `.gemini/settings.json`.
- **Harness Integrity:** Any modification to `.gemini/` or `AGENTS.md` requires explicit user confirmation.

## 🧩 3. Domain Context
- **Root Package:** `com.portfolio.backtest`
- **Domain Focus:** Financial backtesting, stock/ETF market data ingestion, and technical analysis.
- **Data Source:** Primarily Jsoup-based crawlers for market data.

## 🔄 4. Self-Evolution Protocol (SEP)
Continuous improvement and knowledge objectification are managed via `.gemini/skills/self_evolution.md`.
- **Standardize**: Move recurring complex workflows into new skills.
- **Audit**: Regularly review `AGENTS.md` and `GEMINI.md` to ensure they reflect the current architectural state.

## 📊 5. Agile Governance & High-Fidelity Tasking
All autonomous tasking MUST adhere to the hierarchy and quality standards defined in `.gemini/skills/scrum_master_planning.md`.

### Issue Hierarchy
- **Epic**: Strategic objective. Maps to a domain/module.
- **Feature**: A deliverable unit of value with a high-level technical approach.
- **Task (Atomic Unit)**: Must follow the **INVEST** principle and be "Session-Independent".
  - **Self-Contained**: Include specific package paths, class names, and method requirements so any new session can implement it without prior context.
  - **Acceptance Criteria (AC)**: Every Task MUST have a 3-5 item checklist for completion.

### Quality Standards
- **Technical Specificity**: Explicitly mention files, annotations, and logic constraints.
- **Definition of Done (DoD)**: Implementation, Unit Tests (JUnit 5), and successful Gradle build.

## 🚀 6. DevOps & Infrastructure
Professional standards for the Dual-Server, Dual-Database OCI environment.
- **Registry**: Use GitHub Container Registry (GHCR) for all Docker images.
- **Infrastructure**:
  - **Batch Server**: `VM.Standard.E2.1.Micro` + **Batch ATP** (Staging Data).
  - **API Server**: `VM.Standard.E2.1.Micro` + **API ATP** (Refined Data).
- **Deployment**:
  - CI triggers on PR; CD triggers on Merge to `master`.
  - Independent deployment jobs for API and Batch VMs using `appleboy/ssh-action`.
- **Workflow**: Batch server transforms data -> Pushes to API DB -> Notifies API server via REST.

## 🤖 7. Autonomous Development Workflow (10 Steps)
1. **Receive Issue**: Receive an issue number from the user.
2. **Fetch Issue**: Obtain the issue title and body using `gh issue view`.
3. **Understand Content**: Comprehend the requirements and the intent behind the requested fix.
4. **Root Cause Analysis [Regression Point]**: Explore the codebase to identify target files and the root cause.
5. **Solution Plan**: Establish a JSON Action Plan including target files, logic changes, and verification methods.
6. **Isolated Implementation**: Create a `git worktree` to perform code modifications in an isolated environment.
7. **Feedback Loop**: Execute unit tests within the modified path and collect results.
8. **Local Verdict**: If step 7 succeeds, proceed to step 9. If it fails, return to [Step 4: Root Cause Analysis] with error logs (GOTO 4).
9. **Reflect/Push**: Commit changes within the worktree and push to the remote branch.
10. **Final CI Verification**: Monitor results using `gh run watch`. If CI fails, return to [Step 4: Root Cause Analysis] with logs (GOTO 4).

## 👥 8. Sub-Agent Role Definitions
- **Planner**: Responsible for steps 2–5 (Analysis & Design); establishes the overall resolution strategy.
- **Executor**: Responsible for steps 6 and 9 (Physical Implementation & Push); focuses on task execution within the isolated environment.
- **Verifier**: Responsible for steps 7, 8, and 10 (Verification & Regression Verdict); judges success and provides feedback to the analysis phase if necessary.
