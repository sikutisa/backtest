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
