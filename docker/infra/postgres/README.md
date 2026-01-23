# PostgreSQL Infrastructure

This module defines the **PostgreSQL database infrastructure** used for local development.

It is intentionally minimal and environment-agnostic.

---

## Responsibilities

This image is responsible for:
- Providing a PostgreSQL runtime
- Running initialization scripts (schema, users, extensions)

This image is NOT responsible for:
- Data persistence configuration
- Port mapping
- Environment-specific credentials

Those concerns belong to the orchestrator (Docker Compose, Kubernetes).

---

## Initialization scripts

The `init/` directory contains SQL scripts that are executed **once** when the database
is started for the first time and the data directory is empty.

Execution order is alphabetical.

Example use cases:
- Schema creation
- Role creation
- Extensions setup

---

## Volumes and persistence

Persistence is **not defined here**.

Data volumes must be configured in:
- `docker-compose.yml` (local)
- Kubernetes manifests (QA / Prod)

This ensures:
- Image portability
- Clear separation of concerns
- Infrastructure consistency

---

## Usage

This image is intended to be consumed by `docker-compose.yml`.

Example (simplified):

```yaml
services:
  postgres:
    image: project-infrastructure-postgres:16
