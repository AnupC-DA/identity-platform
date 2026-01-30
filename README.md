# identity-platform

Proof-of-concept for **Keycloak**-based identity and SSO using **Organizations** and reusable authentication flows. Supports local auth, LDAP, external IdP (OIDC/SAML), MFA, and passwordless flows.

## Purpose

- Single Keycloak realm per environment with **Organizations** as tenants.
- One SSO plane for all products (OIDC first; SAML where required).
- Multi-tenant with strong isolation; customer never sees Keycloak (custom domain, branding).
- Prove all major Keycloak authentication mechanisms with org-scoped flows.

## Prerequisites

- **Docker** and **Docker Compose** (for local Keycloak + Postgres).
- **Git**.
- (Optional) **Node.js** or **Python** for demo apps.

## Quick start

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/identity-platform.git
   cd identity-platform
   ```

2. **Start Keycloak and Postgres** (once `docker/` is set up)
   ```bash
   cd docker
   docker compose up -d
   ```

3. **Access Keycloak Admin**
   - URL: http://localhost:8080 (or as configured)
   - Create realm, organizations, and clients per the [docs](docs/).

4. **Run demo apps** (once available under `apps/`)
   - See `apps/` for App A (server-side) and App B (SPA) and their READMEs.

## Repository structure

| Folder    | Purpose                                      |
|-----------|----------------------------------------------|
| `docs/`   | Setup, auth flows, troubleshooting, demos    |
| `docker/` | Docker Compose (Keycloak, Postgres, LDAP)   |
| `scripts/`| Automation, realm export/import, provisioning |
| `apps/`   | Demo applications (App A, App B)             |
| `.github/`| CI/CD, issue templates, workflows            |

## Documentation

- Setup and environment: see `docs/` (to be added).
- Auth flows and demo script: see project backlog (EPIC-3, EPIC-4).

## License

Internal / confidential. See your organization’s policy.
