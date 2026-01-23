# =========================================================
# PostgreSQL Infrastructure Image
# =========================================================

FROM postgres:16

# Metadata
LABEL maintainer="aosnaya@company.com"
LABEL database="postgresql"
LABEL version="16"

# ---------------------------------------------------------
# Initialization scripts
# ---------------------------------------------------------
# These scripts run ONLY on first container startup
# when the data directory is empty
COPY init /docker-entrypoint-initdb.d/

# ---------------------------------------------------------
# Default configuration
# ---------------------------------------------------------
# Do NOT define volumes here
# Do NOT expose ports here
