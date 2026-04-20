# Arda Labs

> **Where data flows with intelligence.**

**Arda Labs** xây dựng hệ thống quản trị doanh nghiệp multi-tenant trên nền tảng cloud-native:

- **Micro-Frontend** (Angular + Module Federation)
- **Microservices** (Go + Java/Spring Boot)
- **GitOps** (ArgoCD + K3s)
- **APISIX** API Gateway + Cloudflare Tunnel

---

## Brand

| Thuộc tính      | Giá trị                                               |
| --------------- | ----------------------------------------------------- |
| **Name**        | ARDA Labs                                             |
| **Fonts**       | Space Grotesk (logo) · Inter (text)                   |
| **Colors**      | Cyan `#06B6D4` · Indigo `#6366F1` · Midnight `#0F172A` |
| **Style**       | Minimal · Futuristic · Data-oriented                  |
| **Slogan**      | _"Where data flows with intelligence."_               |

---

# Arda Platform Architecture

```
Browser → Cloudflare Tunnel → APISIX Gateway → [K8s Services]
                                       ├─ mfe-shell    (Angular Host)
                                       ├─ mfe-common   (Angular Remote)
                                       ├─ go-crm       (Go microservice)
                                       └─ ...
```

## CI/CD Flow

```
git push (main) → GitHub Actions
  ├─ lint · test · build (Nx)
  ├─ Docker build + push (GHCR)
  └─ Update tag in arda-infra → ArgoCD auto-sync → K3s deploys
```

## Tech Stack

| Layer        | Technology                                                       |
| :----------- | :--------------------------------------------------------------- |
| **Frontend** | Angular 21 · Module Federation · Rspack · PrimeNG · Tailwind CSS |
| **Backend**  | Go (CRM) · Java 21 / Spring Boot 3.5                             |
| **Infra**    | K3s · ArgoCD · Kustomize · APISIX · Cloudflare Tunnel            |
| **CI/CD**    | GitHub Actions · GHCR · Git-based tag promotion                  |
| **Security** | Cloudflare Zero Trust · APISIX · Keycloak                        |

## Repositories

### Frontend — [arda-mfe](https://github.com/arda-labs/arda-mfe)

Nx monorepo with Angular Module Federation.

| App              | Role                                     |
| :--------------- | :--------------------------------------- |
| `apps/shell`     | Host app — Auth, Layout, Navigation      |
| `apps/common`    | Remote MFE — Shared components & routes  |

### Infrastructure — [arda-infra](https://github.com/arda-labs/arda-infra)

GitOps-managed Kubernetes manifests with Kustomize overlays.

| Component       | Namespace   | Purpose                              |
| :-------------- | :---------- | :----------------------------------- |
| APISIX Gateway  | `gateway`   | API Gateway + routing (admin API)    |
| Cloudflared     | `infra`     | Cloudflare Tunnel ingress            |
| mfe-shell       | `arda-dev`  | Angular shell app (nginx)            |
| mfe-common      | `arda-dev`  | Angular remote MFE (nginx)           |
| go-crm          | `arda-dev`  | CRM microservice (Go)                |

### Backend — [arda-be](https://github.com/arda-labs/arda-be)

Go microservices.

---

## Quick Start

```bash
# 1. Bootstrap K3s cluster
git clone https://github.com/arda-labs/arda-infra
cd arda-infra
./scripts/bootstrap.sh

# 2. Configure APISIX routes
./scripts/apisix-routes.sh

# 3. Setup Cloudflare Tunnel
# Configure tunnel to route arda.io.vn → http://apisix-gateway.gateway:80
```

Push to `main` in `arda-mfe` triggers automatic deployment via CI/CD pipeline.

---

- Website: [arda.io.vn](https://arda.io.vn)
- Contact: **contact@arda.io.vn**
