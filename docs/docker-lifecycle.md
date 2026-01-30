# Docker lifecycle — Start, stop, reset (STORY-0.3)

## Start

From repo root:

```bash
cd docker
cp .env.example .env   # first time only; set POSTGRES_PASSWORD, KC_ADMIN_USERNAME, KC_ADMIN_PASSWORD
docker compose up -d
```

**Expected:** Postgres and Keycloak containers start. Keycloak may take 1–2 minutes to become ready.

## Stop

```bash
cd docker
docker compose down
```

**Expected:** Containers stop; data in `postgres_data` volume is kept.

## Full reset (wipe volumes + restart)

```bash
cd docker
docker compose down -v
docker compose up -d
```

**Expected:** Postgres data is removed; fresh Keycloak + empty DB. Re-run realm/org setup if needed.

## Validate

- **Start:** `docker compose ps` — both services `healthy` or `running`; http://localhost:8080/health/ready returns 200.
- **Stop:** `docker compose ps` — no containers listed.
- **Reset:** After `up -d`, Keycloak login works with credentials from `.env`; no previous realm data.
