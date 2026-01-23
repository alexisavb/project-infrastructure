# Java Runtime (Java 17 + Maven)

This module defines the **standard Java runtime environment** used by all backend services in this repository.

It provides:
- Java 17 (LTS)
- Maven
- Common development utilities

The goal is to ensure **consistent builds and execution** across all environments:
- Local development
- CI/CD pipelines
- Production containers

---

## Why this exists

Instead of installing Java and Maven directly on each developer machine, we:

- Standardize the Java version
- Avoid "works on my machine" issues
- Make onboarding trivial
- Align local, CI, and production environments

Docker is the **only required dependency**.

---

## What this image is (and is not)

### ✅ This image IS:
- A base runtime for Java services
- Reusable across multiple microservices
- Suitable for local development and CI

### ❌ This image is NOT:
- A runnable application
- A production service container by itself
- Tied to any specific backend

---

## How it is used

Backend services will **extend this image** in their own Dockerfiles.

Example (simplified):

```dockerfile
FROM project-infrastructure-java:17

COPY target/app.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]
