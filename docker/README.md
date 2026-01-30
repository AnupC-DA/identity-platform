# Docker — Keycloak 26.5.2 + Postgres (STORY-0.2)

Runs Keycloak with Postgres for local DAIS / identity-platform development. Organizations feature and health endpoints are enabled.

## Prerequisites

- Docker and Docker Compose v2+
- `.env` file (see below)

## Setup

1. **Copy env template and set secrets**

   ```bash
   cd docker
   cp .env.example .env
   # Edit .env: set POSTGRES_PASSWORD, KC_ADMIN_USERNAME, KC_ADMIN_PASSWORD (no real secrets in .env.example)
   ```

2. **Start**

   ```bash
   docker compose up -d
   ```

3. **Validate startup**

   - Postgres: `docker compose ps` — `postgres` should be `healthy`.
   - Keycloak: wait until `keycloak` is `healthy` (or running). Admin UI: http://localhost:8080 (or `KC_HTTP_PORT` from `.env`).
   - Health: http://localhost:9000/health/ready (management port) or http://localhost:8080/health/ready — should return 200. If the Keycloak image has no `curl`, the container may show unhealthy; remove the `healthcheck` block in `docker-compose.yml` if needed.

4. **Stop**

   ```bash
   docker compose down
   ```

5. **Full reset (wipe volumes + restart)**

   ```bash
   docker compose down -v
   # Optionally delete .env and re-copy from .env.example, then:
   docker compose up -d
   ```

## Tasks (STORY-0.2) — Done when

| Task   | Done when |
|--------|-----------|
| 0.2.1  | Both services defined in `docker-compose.yml` ✓ |
| 0.2.2  | Postgres uses volume `postgres_data` — data survives restart ✓ |
| 0.2.3  | Secrets in `.env` only — no secrets in compose file ✓ |
| 0.2.4  | `.env.example` documents required variables ✓ |
| 0.2.5  | Keycloak health: `--health-enabled=true`, `/health/ready` responds ✓ |
| 0.2.6  | Organizations: `--features=organization` ✓ |
| 0.2.7  | `docker compose up -d` starts Keycloak and Postgres ✓ |
| 0.2.8  | `docker compose down` clean shutdown ✓ |
