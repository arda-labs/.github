# Arda Labs

> Where data flows with intelligence.

Arda Labs builds a cloud-native, multi-tenant financial operations platform.
The codebase is organized as independent repositories: backend Go microservices,
a frontend React Module Federation shell, and GitOps infrastructure manifests.

## Current Architecture

```text
Browser
  -> Cloudflare Tunnel (cloudflared)
  -> Traefik Ingress (K3s cluster)
     |-- auth-gateway -> Ory Hydra / Kratos (identity)
     |-- web (shell MFE, port 5000)
     |-- mfe-iam (5101) | mfe-platform (5102) | mfe-finance (5103)
     |-- mfe-account (5104) | mfe-hrm (5105)
     |-- mfe-workflow (5106) | mfe-crm (5107)
     |-- iam-service (8080/9090) | platform-service (8080/9090)
     |-- finance-service (8080)  | workflow-service (8080/9090)
     |-- crm-service (8080/9090) | hrm-service (8080)
     |-- media-service (8080)    | notification-service (8080)
  -> CloudNativePG (Postgres 18, 3-node HA)
  -> NATS | Valkey | Garage S3 | Zeebe (Camunda 8)
```

## Active Repositories

| Repository | Purpose |
| --- | --- |
| [`arda-be`](https://github.com/arda-labs/arda-be) | Go 1.26 microservices, shared libs, protobuf definitions |
| [`arda-mfe`](https://github.com/arda-labs/arda-mfe) | React 19 MFE shell + 7 remotes via Module Federation |
| [`arda-infra`](https://github.com/arda-labs/arda-infra) | K3s manifests, ArgoCD apps, Traefik config, Ory auth |
| [`.github`](https://github.com/arda-labs/.github) | Organization profile and GitHub metadata |

## Platform Map

| Module | Type | Stack |
| --- | --- | --- |
| `shell` | MFE host | React 19, Vite 8, Module Federation |
| `mfe-iam` | Remote MFE | Identity & access admin |
| `mfe-platform` | Remote MFE | Master data & platform admin |
| `mfe-finance` | Remote MFE | Finance operations |
| `mfe-account` | Remote MFE | Profile & account settings |
| `mfe-hrm` | Remote MFE | HRM admin |
| `mfe-workflow` | Remote MFE | BPMN workflow admin |
| `mfe-crm` | Remote MFE | CRM & workbench |

| Service | Language | Description |
| --- | --- | --- |
| `auth-gateway` | Go | API gateway, OAuth/OIDC proxy, forward-auth, session |
| `iam-service` | Go | Identity, RBAC (Casbin), MFA, audit |
| `platform-service` | Go | Platform runtime, NATS events |
| `finance-service` | Go | Finance domain operations |
| `workflow-service` | Go | Workflow engine facade (Zeebe 8.5) |
| `crm-service` | Go | Customer relationship management |
| `hrm-service` | Go | Human resources management |
| `media-service` | Go | Media storage (Garage S3) |
| `notification-service` | Go | Notifications, Web Push, NATS |

## Tech Stack

| Layer | Technology |
| --- | --- |
| Frontend | React 19, TypeScript 6, Vite 8, Module Federation, Tailwind CSS 4, shadcn/ui, TanStack Query, Zustand, i18next |
| Backend | Go 1.26, gRPC, PostgreSQL, pressly/goose, Custom HTTP framework (`arda-http`), NATS, Zeebe 8.5 |
| Identity | Ory Hydra (OAuth2/OIDC) + Ory Kratos (identity/password) |
| Storage | CloudNativePG (Postgres 18, 3-node HA), Valkey (Redis fork), Garage (S3-compatible) |
| Gateway & Ingress | Traefik with forward-auth middleware |
| GitOps | ArgoCD, Kustomize, Image Updater |
| Runtime | K3s cluster (3 nodes), Cloudflare Tunnel, GHCR images |

## Runtime Routes

| Route | Target |
| --- | --- |
| `/` | Web (MFE shell) — public paths |
| `/auth/*`, `/login*`, `/callback*`, `/consent` | Web (no auth) |
| `/assets/*`, `/mfes/*` | Web static assets & remote entry points |
| `/api/*` | Auth gateway → backend services |

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
