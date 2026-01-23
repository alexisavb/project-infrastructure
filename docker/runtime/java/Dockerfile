# =========================================================
# Base Java Runtime for Backend Services
# Java 17 + Maven
# =========================================================

FROM eclipse-temurin:17-jdk-jammy

# Metadata
LABEL maintainer="aosnaya@company.com"
LABEL runtime="java"
LABEL java.version="17"
LABEL build.tool="maven"

# ---------------------------------------------------------
# System dependencies
# ---------------------------------------------------------
RUN apt-get update && \
    apt-get install -y \
        maven \
        curl \
        bash \
        git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# ---------------------------------------------------------
# Maven configuration
# ---------------------------------------------------------
ENV MAVEN_HOME=/usr/share/maven
ENV MAVEN_CONFIG=/root/.m2

# ---------------------------------------------------------
# Working directory
# ---------------------------------------------------------
WORKDIR /workspace

# ---------------------------------------------------------
# Default command (overridden by child images)
# ---------------------------------------------------------
CMD ["bash"]