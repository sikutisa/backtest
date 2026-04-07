# System Architecture: Backtest Platform (OCI Distributed)

This document defines the structural blueprints for the distributed OCI environment, emphasizing physical isolation and unidirectional data flow.

## 1. High-Level Topology (Unidirectional Flow)
The system utilizes OCI Free Tier resources with a strict separation between data ingestion (Batch) and data serving (API).

```text
       +-------------------------+
       |   External Providers    |
       |  (SEIBro, KRX Data API) |
       +-----------+-------------+
                   |
                   | (1) Crawling (XML/JSON)
                   v
+---------------------------------------+          +-----------------------+
|         OCI Batch Env (VM 1)          |          |         CI/CD         |
|  [module-batch] (1GB RAM + Swap)      |          |    (GitHub Actions)   |
|      +                                |          +-----------+-----------+
|      | (2) Store Raw                  |                      |
|      v                                |                      | Push
|  [ATP 1: Batch ATP] (Raw Data)        |                      v
|      +                                |          +-----------------------+
|      | (3) Read & Transform           |          |  GH Container (GHCR)  |
|      v                                |          +-----------+-----------+
|  [module-batch] (Processing)          |                      |
|      +                                |                      | Deploy
|      | (4) Push Refined Data          |                      |
+------|--------------------------------+                      |
       |                                                       |
       v                                                       v
+-------------------------------+          +-------------------------------+
|       ATP 2 (API ATP)         | <--------+       OCI API Env (VM 2)      |
|        (Domain Data)          |  Serve   |  [module-api] (1GB + Swap)    |
+-------------------------------+   (5)    +---------------+---------------+
                                                           |
                                                           | (6) Response
                                                           v
                                                     +------------+
                                                     |  End User  |
                                                     +------------+

[Infrastructure Constraints & Notes]
- VM 1 & VM 2: VM.Standard.E2.1.Micro (1 OCPU, 1 GB RAM).
- Memory Management: Swap space (2GB+) is required to prevent OOM on Java 25.
- DB Isolation: module-batch is the master actor connecting to BOTH ATP 1 and ATP 2.
- Decoupling: No direct REST/synchronous calls between VM 1 and VM 2.
```

## 2. Refined Data Workflow
1.  **Crawling**: `module-batch` (VM 1) fetches raw data from **SEIBro** (XML) and **KRX** (JSON).
2.  **Staging**: Raw data is stored in **ATP 1 (Batch ATP)**.
3.  **Refining**: `module-batch` reads raw data from ATP 1 and performs domain transformation.
4.  **Synchronization**: `module-batch` pushes the refined **Domain Data** into **ATP 2 (API ATP)**.
5.  **Serving**: `module-api` (VM 2) reads exclusively from **ATP 2** to serve requests.
6.  **Response**: End users receive data via REST endpoints provided by `module-api`.

## 3. Infrastructure Specifications
- **Compute A (Batch)**: `VM.Standard.E2.1.Micro` (1 OCPU, 1 GB RAM, Linux).
- **Compute B (API)**: `VM.Standard.E2.1.Micro` (1 OCPU, 1 GB RAM, Linux).
- **Database A (Batch ATP)**: Always Free Autonomous Transaction Processing (20 GB) - Staging area.
- **Database B (API ATP)**: Always Free Autonomous Transaction Processing (20 GB) - Production area.

## 4. Architectural Principles
- **Physical Isolation**: The staging (Batch) and production (API) databases are physically separate instances.
- **Unidirectional Flow**: Data moves from External -> Batch -> Staging -> Refined -> API.
- **Resource Discipline**: Java 25 is tuned with `-Xmx` and `-XX:MaxMetaspaceSize` to fit within the 1GB RAM limitation, supplemented by disk swap.
