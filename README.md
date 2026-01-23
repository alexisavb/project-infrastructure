# Project Infrastructure

## Overview

This repository defines the **infrastructure and runtime foundation** for the project using a **monorepo approach**.

Its primary goal is to provide a **reproducible, consistent, and portable development environment** that can be used by all developers, CI pipelines, and non-production environments without relying on host-level installations of runtimes such as Java, Maven, Node, or databases.

The repository is designed following **infrastructure-as-code principles**, with a strong focus on clarity, separation of responsibilities, and scalability.

---

## Goals

- Provide a **single source of truth** for local development infrastructure
- Eliminate “works on my machine” issues
- Standardize runtimes (Java, Maven, databases)
- Enable fast onboarding of new developers
- Serve as the foundation for CI/CD, QA, and production environments
- Maintain clear boundaries between:
  - Application code
  - Runtime definitions
  - Infrastructure configuration

---

## Non-Goals

This repository is **not** intended to:

- Replace IDEs or developer tooling (IntelliJ, VS Code, etc.)
- Store secrets or environment-specific credentials
- Contain production-only infrastructure definitions
- Act as a deployment artifact by itself

---

## Repository Structure

```md
project-infrastructure/
├─ docker/                # Runtime and infrastructure definitions
│  ├─ runtime/            # Language runtimes (e.g. Java, Node)
│  └─ infra/              # Databases and supporting services
│
├─ backend/               # Backend application source code
├─ frontend/              # Frontend application source code
│
├─ scripts/               # Helper scripts for local development
│
├─ docker-compose.yml     # Local environment orchestration
├─ .env.example           # Environment variable contract
├─ README.md              # This document
└─ .gitignore
```

---

## Architecture Principles

This project follows these non-negotiable principles:

1. **Runtime isolation**  
   All runtimes (Java, Maven, Node, PostgreSQL, etc.) run inside containers.  
   The host machine only requires Docker.

2. **Separation of concerns**  
   - Application code does not define infrastructure  
   - Infrastructure does not contain business logic  
   - Runtime images are reusable and standardized  

3. **Declarative infrastructure**  
   The desired state of the local environment is described declaratively using Docker Compose.

4. **Reproducibility over convenience**  
   Consistency across machines and environments is prioritized over ad-hoc local optimizations.

5. **Environment parity**  
   Local development closely mirrors non-production environments to reduce deployment risk.

---

## Local Development Philosophy

- Developers write and edit code on the host machine using their IDE of choice.
- Applications run inside containers using standardized runtimes.
- Databases and supporting services are fully containerized.
- Configuration is injected via environment variables.

The only required tools on the host system are:
- Docker (Docker Desktop or compatible)
- A code editor or IDE

---

## Configuration Management

All configuration is handled via environment variables.

- `.env.example` documents **all required variables**
- Each developer creates their own `.env` file locally
- `.env` files are **never committed**
- No secrets are stored in the repository

---

## Usage (High Level)

At a conceptual level, the local environment is started using Docker Compose.

The exact commands and service definitions are documented in their respective directories and will evolve as the system grows.

---

## CI/CD and Future Environments

This repository is designed to integrate seamlessly with CI/CD pipelines (e.g. GitHub Actions).

While Docker Compose is used for local development, the same images and principles are intended to be reused in:
- CI pipelines
- QA / Staging environments
- Production orchestration platforms (e.g. Kubernetes or managed container services)

---

## Contribution Guidelines

- Infrastructure changes must be explicit and well-documented
- Runtime changes (e.g. Java version upgrades) must be coordinated
- Backward compatibility should be considered for shared runtimes
- Pull requests should be atomic and self-contained

---

## 🚀 Running the project locally

### Prerequisites
- Docker Desktop installed and running

Clone the repository and enter the project directory:

```bash
git clone <repository-url>
cd project-infrastructure
```

Ensure Docker Desktop is installed and running:

```bash
docker info
```

Create the environment variables file:

```bash
p .env.example .env
```

Build and start all containers:

```bash
docker compose up -d --build
```

List running containers:

```bash
docker ps
```

Access the Java container shell:

```bash
docker exec -it java-runtime bash
```

Exit the container shell:

```bash
exit
```

Stop all containers:

```bash
docker compose down
```

Stop containers and remove volumes:

```bash
docker compose down -v
```

