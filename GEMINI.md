# GEMINI.md - Backtest Project Context

## Project Overview
This project is a **Portfolio Backtest Engine and Crawler** built with **Java 25** and **Spring Boot 4.0.3**. It is designed with a multi-module architecture to separate the API, batch processing, and core domain logic.

### Main Technologies
- **Language:** Java 25 (Temurin/OpenJDK)
- **Framework:** Spring Boot 4.0.3
- **Build Tool:** Gradle (Multi-module)
- **Database:** PostgreSQL (with Spring Data JPA)
- **Batch Processing:** Spring Batch (for crawlers or data analysis)
- **Other:** Lombok (boilerplate reduction), Spring Boot Actuator (monitoring)

## Architecture

```text
backtest-portfolio (루트 프로젝트)
 ├── build.gradle
 ├── settings.gradle
 │
 ├── module-core
 │    ├── src/main/java/com/portfolio/backtest/core
 │    │    ├── domain       (JPA Entity: Stock, DailyPrice 등)
 │    │    ├── repository   (Spring Data JPA 기본 Repository)
 │    │    └── config       (DB 연결, JPA 공통 설정)
 │    └── src/main/resources
 │         └── application-core.yml (DB 접속 정보 등)
 │
 ├── module-api
 │    ├── src/main/java/com/portfolio/backtest/api
 │    │    ├── ApiApplication.java  (스프링부트 실행 클래스)
 │    │    ├── controller   (REST API Endpoints)
 │    │    ├── service      (백테스트 비즈니스 로직)
 │    │    └── repository   (백테스트용 JdbcTemplate 복잡한 조회 쿼리)
 │    └── src/main/resources
 │         └── application.yml      (API 서버 포트, 로깅 설정 등)
 │
 └── module-batch
      ├── src/main/java/com/portfolio/backtest/batch
      │    ├── BatchApplication.java (스프링부트 실행 클래스)
      │    ├── job          (Spring Batch Job/Step 설정)
      │    ├── crawler      (Jsoup 연동 로직)
      │    └── repository   (JdbcTemplate.batchUpdate 등 대량 적재 로직)
      └── src/main/resources
           └── application.yml      (배치 메타데이터 설정 등)
```

The project follows a multi-module structure to ensure scalability and separation of concerns:

- **`module-core`**: Houses common business logic, domain models (JPA), and base repositories.
- **`module-api`**: Handles REST API endpoints, backtest business logic, and complex queries via JdbcTemplate.
- **`module-batch`**: Contains batch jobs for data crawling (Jsoup), processing, and high-volume data ingestion.

## Building and Running

### Prerequisites
- Java 25 JDK or higher.
- Gradle (provided via `./gradlew`).

### Key Commands
- **Build the whole project:**
  ```bash
  ./gradlew build
  ```
- **Run the application:**
  ```bash
  ./gradlew bootRun
  ```
- **Run all tests:**
  ```bash
  ./gradlew test
  ```
- **Clean build artifacts:**
  ```bash
  ./gradlew clean
  ```

## Development Conventions
- **Multi-module dependency:** Standard Gradle `implementation` and `testImplementation` project dependencies should be used to share code between modules.
- **Testing:** The project uses JUnit 5 (JUnit Platform). All new features should be accompanied by relevant test cases (unit/integration).
- **Style:** Lombok is used for data objects (`@Data`, `@Getter`, `@Setter`, etc.) and constructors (`@RequiredArgsConstructor`).
- **Configuration:** Main application settings are located in `src/main/resources/application.yaml`.

## TODO / Roadmap
- [ ] Implement core backtesting engine in `module-core`.
- [ ] Add data crawlers in `module-batch`.
- [ ] Expose backtest results via REST API in `module-api`.
- [ ] Set up database migration (Flyway or Liquibase).
- [ ] Configure Docker environment for PostgreSQL.
