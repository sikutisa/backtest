---
name: devops_pipeline_generator
description: Generate and manage CI/CD pipelines for GitHub Actions and OCI.
---

# Skill: DevOps Pipeline Generator
 (OCI & GHCR)

This skill generates high-fidelity GitHub Actions workflows for multi-module Java projects (Spring Boot) targeting GHCR and OCI environments.

## 🛠 Prerequisites
- Dockerized modules (`module-api`, `module-batch`).
- SSH access to the OCI instance.
- GitHub repository configured for GHCR.

## 🔄 Workflow Generation SOP

### 1. CI Workflow (`ci.yml`)
Trigger: PR to `master`.
- Task: Build and test both modules (`module-api`, `module-batch`).
- Command: `./gradlew check test`.

### 2. CD Workflow (`cd.yml`)
Trigger: Merge to `master`.
- **Build & Push**: Build Docker images for both modules and push to GHCR.
- **Deploy VM-Batch**: 
  - Host: `OCI_BATCH_IP`.
  - Action: Pull `module-batch` image, restart with `docker-compose`.
- **Deploy VM-API**: 
  - Host: `OCI_API_IP`.
  - Action: Pull `module-api` image, restart with `docker-compose`.

### 3. Remote Execution (`run-crawler.yml`)
Trigger: Manual (`workflow_dispatch`).
- Task: Execute specific batch job on `OCI_BATCH_IP`.

## 📋 Necessary GitHub Secrets Checklist
1. `GHCR_TOKEN`: PAT for registry write access.
2. `OCI_BATCH_IP`, `OCI_API_IP`: Target OCI instance IPs.
3. `SSH_USER`: SSH login username.
4. `SSH_PRIVATE_KEY`: Private key for OCI.
5. `BATCH_DB_URL`, `BATCH_DB_USER`, `BATCH_DB_PASSWORD`: For Batch ATP.
6. `API_DB_URL`, `API_DB_USER`, `API_DB_PASSWORD`: For API ATP.

## 🏗 4. OCI Infrastructure & Database Architecture
Professional standards for the Dual-Server, Dual-Database OCI environment.

- **Registry**: Use GitHub Container Registry (GHCR) for all Docker images.
- **Infrastructure**:
  - **Batch Server**: `VM.Standard.E2.1.Micro` (AMD) + **Batch ATP** (Staging Data).
  - **API Server**: `VM.Standard.E2.1.Micro` (AMD) + **API ATP** (Refined Data).
- **Workflow**: 
  1. Batch server transforms/crawls data.
  2. Pushes to API DB (Refined table).
  3. Notifies API server via REST to clear caches.

## 🚀 5. Deployment Protocol
- CI triggers on PR; CD triggers on Merge to `master`.
- Independent deployment jobs for API and Batch VMs using `appleboy/ssh-action`.
