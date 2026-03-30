# AGENTS.md - The Sovereign Constitution of Autonomous Agents

This document is the **Single Source of Truth (SSoT)** for all AI agents operating within this workspace. It defines the technical boundaries, behavioral ethics, and the evolution protocol for autonomous development.

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
- **No-Secret Policy:** Never log or commit credentials. Use `.env`, system variables, or Spring Cloud Config.
- **Credential Review Process:**
    - **Self-Audit:** Before any `git commit`, perform a `git diff --staged` to scan for keywords: `key`, `password`, `secret`, `token`, `auth`, `api_key`.
    - **Configuration Isolation:** Sensitive values in `application.yml` MUST be replaced with placeholders (e.g., `${DB_PASSWORD}`) and documented in a `*.sample` file.
    - **Gitignore Enforcement:** Ensure `.env`, `.idea`, `build/`, and any local-only config files are strictly tracked in `.gitignore`.
- **Tool Restriction:** All `run_shell_command` calls must adhere to the allow-list in `.gemini/settings.json`.
- **Harness Integrity:** Any modification to `.gemini/` or `AGENTS.md` requires explicit user confirmation.
- **Verification:** Regularly run `git grep` for accidental leaks of sensitive patterns in the codebase.

## 🧩 3. Domain Context
- **Root Package:** `com.portfolio.backtest`
- **Domain Focus:** Financial backtesting, stock/ETF market data ingestion, and technical analysis.
- **Data Source:** Primarily Jsoup-based crawlers for market data.

## 🔄 4. Self-Evolution Protocol (SEP)
- **Objectify Knowledge:** "반복되는 복잡한 워크플로우 발견 시, 즉시 `.gemini/skills/` 하위에 새로운 SOP(Standard Operating Procedure)를 생성하여 지식을 객관화하라."
- **Identify Patterns:** Notice recurring tasks and propose new `SKILL.md` templates.
- **Modularize Knowledge:** Refactor complex logic into specialized skills in `.gemini/skills/`.
- **Audit History:** Regularly review `AGENTS.md` and `GEMINI.md` to ensure they reflect the current architectural state.
- **Knowledge Sharing:** Update the `Expert Registry` whenever a new professional domain is mastered.
