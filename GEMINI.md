# GEMINI.md - Machine-Readable Instruction Layer

## 🎯 Global Directives
1. **Primary SSoT:** All reasoning, strategy, and execution MUST prioritize the directives in `./AGENTS.md`.
2. **Security Verification:** Before executing any tool (especially `run_shell_command`), confirm its adherence to the security policy in `.gemini/settings.json`.
3. **Consistency:** Adhere to existing patterns in `module-core`, `module-api`, and `module-batch`.

## 🛠 Core Tech Stack (Mirror from AGENTS.md)
- **Runtime:** Java 25 (OpenJDK)
- **Framework:** Spring Boot 4.0.3 / Dependency Management 1.1.7
- **Modules:** `module-core` (Domain/JPA), `module-api` (REST/Biz), `module-batch` (Jsoup/Batch)
- **Database:** PostgreSQL (Port 5432)

## 🗺 Module Map
- **core**: Entity mapping (`Stock`, `DailyPrice`), JPA Repositories, DB Config.
- **api**: `ApiApplication`, REST Controllers, Backtest Service, `JdbcTemplate` for complex queries.
- **batch**: `BatchApplication`, Spring Batch Jobs, Jsoup Crawlers, Bulk Ingestion.

## 📌 Development Conventions
- **Package:** `com.portfolio.backtest.[module]`
- **Patterns:** Use Lombok (`@Data`, `@RequiredArgsConstructor`), JUnit 5 for tests.
- **Config:** Core settings in `application-core.yml`; app-specific in `application.yml`.
- **Validation:** Always verify changes with `./gradlew build` using Java 25.

## 🚀 Task State
- [x] Initial Project Restructuring (Multi-module)
- [x] Java 25 / Spring Boot 4.0.3 Environment Setup
- [x] Apache 2.0 License & README
- [x] **Harness Architecture Setup (v1.0)**: AGENTS.md, GEMINI.md (updated), Security settings, Skill registry.
- [ ] Define `Stock` & `DailyPrice` Entities (`module-core`)
- [ ] Implement Jsoup Crawler Logic (`module-batch`)
- [ ] Build Backtest Engine Logic (`module-api`)
- [ ] Add Flyway Migrations & Docker Compose

## 💡 Key Knowledge
- Root application package is `com.portfolio.backtest`.
- `module-api` and `module-batch` both include the `core` profile to load shared DB settings.
