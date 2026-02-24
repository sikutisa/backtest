# Portfolio Backtest Engine & Crawler

A high-performance, multi-module portfolio backtesting engine and data crawler built with **Java 25** and **Spring Boot 4.0.3**.

## 🚀 Overview

This project is designed to crawl historical stock data, store it in a robust PostgreSQL database, and provide a flexible engine for backtesting investment strategies. The architecture is split into specialized modules to ensure scalability and maintainability.

## 🏗 Architecture

The project follows a clean multi-module Gradle structure:

- **`module-core`**: The foundational layer containing JPA entities (`Stock`, `DailyPrice`), base repositories, and core database configurations.
- **`module-api`**: The web layer providing RESTful endpoints for executing backtests and retrieving results.
- **`module-batch`**: The data acquisition layer utilizing Spring Batch and Jsoup for high-volume stock data crawling and ingestion.

### Directory Structure
```text
backtest-portfolio
 ├── module-core
 │    ├── domain (JPA Entities)
 │    ├── repository (Spring Data JPA)
 │    └── config (DB & JPA Configuration)
 ├── module-api
 │    ├── controller (REST Endpoints)
 │    ├── service (Backtest Logic)
 │    └── repository (Complex JdbcTemplate queries)
 └── module-batch
      ├── job (Spring Batch Jobs)
      ├── crawler (Jsoup Logic)
      └── repository (Batch Ingestion)
```

## 🛠 Tech Stack

- **Language:** Java 25 (OpenJDK)
- **Framework:** Spring Boot 4.0.3
- **Build Tool:** Gradle 9.3+
- **Database:** PostgreSQL
- **Persistence:** Spring Data JPA & JdbcTemplate
- **Batch Processing:** Spring Batch
- **Web:** Spring Web (MVC)
- **Crawling:** Jsoup
- **Utilities:** Lombok

## 🚦 Getting Started

### Prerequisites
- Java 25 JDK
- PostgreSQL (Running on `localhost:5432` by default)

### Build
To build the entire project:
```bash
./gradlew build
```

### Run
- **API Server:**
  ```bash
  ./gradlew :module-api:bootRun
  ```
- **Batch Jobs:**
  ```bash
  ./gradlew :module-batch:bootRun
  ```

## 📄 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for more details.
