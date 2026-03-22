# Portfolio Backtest Engine & Crawler

A portfolio backtesting backend and data crawler built with **Java 25** and **Spring Boot 4.0.3**.

## 🚀 Overview

This project is designed to crawl historical stock data from the Korea Exchange (KRX), store it in a robust PostgreSQL database, and provide a flexible engine for backtesting investment strategies. The architecture is split into specialized modules to ensure scalability and maintainability.

## 🏗 Architecture

The project follows a clean multi-module Gradle structure with a shared core for domain logic and persistence.

### Module Breakdown
- **`module-core`**: The foundational layer containing JPA entities (`Stock`, `DailyPrice`), base repositories, and core database configurations. Shared by both the API and Batch modules.
- **`module-api`**: The web layer providing RESTful endpoints for executing backtests and retrieving results.
- **`module-batch`**: The data acquisition layer utilizing Spring Batch and Jsoup for high-volume stock data crawling and ingestion.

### Directory Structure
```text
backtest
 ├── module-core
 │    └── com.portfolio.backtest.core
 │         ├── config (DB & Shared JPA Configuration)
 │         ├── domain (JPA Entities: Stock, DailyPrice)
 │         └── repository (Spring Data JPA)
 ├── module-api
 │    └── com.portfolio.backtest.api
 │         ├── controller (REST Endpoints)
 │         ├── service (Backtest Logic)
 │         └── repository (Complex JdbcTemplate queries)
 └── module-batch
      └── com.portfolio.backtest.batch
           ├── job (Spring Batch Jobs)
           ├── crawler (Jsoup Logic)
           └── repository (Batch Ingestion)
```

## 🛠 Tech Stack

- **Runtime:** Java 25 (OpenJDK)
- **Framework:** Spring Boot 4.0.3 / Spring Batch / Spring Data JPA
- **Database:** PostgreSQL (v16+)
- **Crawling:** Jsoup 1.18.3
- **Build Tool:** Gradle 9.3+
- **Utilities:** Lombok, JUnit 5

## 📡 Data Sources (KRX)

This project utilizes historical market data specifications provided by **KRX (Korea Exchange)**. Detailed documentation for each data source can be found in the [docs/api/](docs/api/) directory.

- **KRX Stocks Daily Trade Data** ([Spec](docs/api/stk_daily_trade_spec.md))
- **KRX ETF Daily Trade Data** ([Spec](docs/api/etf_daily_trade_spec.md))

## ⚙️ Configuration

The project uses a hierarchical configuration approach:
- **`module-core/src/main/resources/application-core.yml`**: Contains shared database, JPA, and logging settings.
- **`module-[api|batch]/src/main/resources/application.yml`**: Contains module-specific application settings.

## 🚦 Getting Started

### Prerequisites
- Java 25 JDK
- PostgreSQL (Running on port `5432` by default)

### Build
To build all modules:
```bash
./gradlew build
```

### Run
- **Start the API Server:**
  ```bash
  ./gradlew :module-api:bootRun
  ```
- **Run Crawler Batch Jobs:**
  ```bash
  ./gradlew :module-batch:bootRun
  ```

## 📄 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for more details.
