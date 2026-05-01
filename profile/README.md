# Arda Labs

> Where data flows with intelligence.

Arda Labs builds a cloud-native, multi-tenant financial and banking platform.
The current codebase is organized as an application monorepo plus a separate
GitOps infrastructure repository.

## Current Architecture

```text
Browser
  -> Cloudflare / local APISIX (9080)
  -> APISIX Gateway
     |-- mfe-shell (4200)
     |-- mfe-iam (4201)
     |-- mfe-mdm (4202)
     |-- iam-service (8000)
     |-- mdm-service (8001)
     |-- crm-service (8010)
  -> PostgreSQL + Zitadel on thinkcenter
```

## Active Repositories

| Repository | Purpose |
| --- | --- |
| [`arda`](https://github.com/arda-labs/arda) | Application monorepo: Angular MFEs, Go services, Java 25 services, shared libs, docs, CI |
| [`arda-infra`](https://github.com/arda-labs/arda-infra) | GitOps manifests, APISIX routes, ArgoCD apps, runtime config, local APISIX |
| [`.github`](https://github.com/arda-labs/.github) | Organization profile and GitHub metadata |

## Current Modules

| Module | Status | Port (Dev) |
| --- | --- | --- |
| `mfe-shell` | Active Angular host app | 4200 |
| `mfe-iam` | Active Angular remote MFE | 4201 |
| `mfe-mdm` | Active Angular remote MFE | 4202 |
| `iam-service` | Active Go/Kratos service | 8000 / 9000 |
| `mdm-service` | Active Go/Kratos service | 8001 / 9001 |
| `crm-service` | Active Java 25 service | 8010 / 9010 |

## Tech Stack

| Layer | Current technology |
| --- | --- |
| Frontend | Angular 21, Native Federation, PrimeNG, Tailwind CSS |
| Go backend | Go 1.26, Kratos, pgx, protobuf, Wire |
| Java backend | Java 25 (LTS), Spring Boot 4.0.6, Virtual Threads (Loom), Flyway |
| Gateway | Apache APISIX |
| Identity | Zitadel |
| GitOps | ArgoCD, Kustomize |
| Runtime | K3s on `thinkcenter`, GHCR images |

## Runtime Routes

| Route | Target |
| --- | --- |
| `/*` | Shell MFE |
| `/mfe-iam/*` | IAM remote assets |
| `/mfe-mdm/*` | MDM remote assets |
| `/api/v1/*` | IAM service |
| `/api/v1/mdm/*` | MDM service |

## Brand

| Attribute | Value |
| --- | --- |
| Name | ARDA Labs |
| Fonts | Space Grotesk for logo, Inter for text |
| Colors | Cyan `#06B6D4`, Indigo `#6366F1`, Midnight `#0F172A` |
| Style | Minimal, data-oriented, operational |
| Slogan | Where data flows with intelligence. |

## Links

- Website: [arda.io.vn](https://arda.io.vn)
- Contact: contact@arda.io.vn
