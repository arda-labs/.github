# Arda Labs

> Where data flows with intelligence.

Arda Labs builds a cloud-native, multi-tenant financial and banking platform.
The current codebase is organized as an application monorepo plus a separate
GitOps infrastructure repository.

## Current Architecture

```text
Browser
  -> Cloudflare / local APISIX
  -> APISIX Gateway
     |-- mfe-shell
     |-- mfe-iam
     |-- mfe-mdm
     |-- iam-service
     |-- mdm-service
  -> PostgreSQL + Zitadel on thinkcenter
```

## Active Repositories

| Repository | Purpose |
| --- | --- |
| [`arda`](https://github.com/arda-labs/arda) | Application monorepo: Angular MFEs, Go services, Java/Kotlin prototypes, shared libs, docs, CI |
| [`arda-infra`](https://github.com/arda-labs/arda-infra) | GitOps manifests, APISIX routes, ArgoCD apps, runtime config, local APISIX |
| [`.github`](https://github.com/arda-labs/.github) | Organization profile and GitHub metadata |

Older split-repo names such as `arda-mfe`, `arda-be`, and `arda-core` are not
the active source of truth.

## Current Modules

| Module | Status |
| --- | --- |
| `mfe-shell` | Active Angular host app |
| `mfe-iam` | Active Angular remote MFE |
| `mfe-mdm` | Active Angular remote MFE |
| `iam-service` | Active Go/Kratos service |
| `mdm-service` | Active Go/Kratos service |
| `accounting_tmp` | Java/Kotlin accounting prototype |

## Tech Stack

| Layer | Current technology |
| --- | --- |
| Frontend | Angular 21, Native Federation, PrimeNG, Tailwind CSS |
| Go backend | Go 1.26, Kratos, pgx, protobuf, Wire |
| Java prototype | Kotlin/Java 21, Gradle |
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
