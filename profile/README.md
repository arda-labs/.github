# 🧠 Arda Labs

> **Where data flows with intelligence.**

**Arda Labs** là tổ chức công nghệ tiên phong trong:

- Hệ thống **quản lý dữ liệu** và **báo cáo thông minh**
- Ứng dụng **AI** và **phân tích thống kê chuyên sâu**
- Xây dựng **giải pháp microservice hiện đại** và mở rộng linh hoạt

---

### 🧩 Nhận diện thương hiệu

| Thành phần      | Nội dung                                             |
| --------------- | ---------------------------------------------------- |
| **Logo name**   | `ARDA Labs`                                          |
| **Font chính**  | Space Grotesk (logo), Inter (text)                   |
| **Màu chủ đạo** | Cyan `#06B6D4` · Indigo `#6366F1` · Midnight `#0F172A` |
| **Phong cách**  | Minimal · Futuristic · Data-oriented                 |
| **Slogan**      | _"Where data flows with intelligence."_              |

---

# Arda Platform — Multi-tenant Enterprise System

Hệ thống quản trị doanh nghiệp đa tenant, mỗi tenant được cô lập hoàn toàn (Separate Database + Dedicated Keycloak Realm), chạy trên nền tảng microservice hiện đại với API Gateway, Kafka event bus và React Micro-Frontend.

## 🏗 Kiến trúc hệ thống

```
Browser → APISIX Gateway → [Internal JWT] → Microservices → PostgreSQL (per-tenant)
                ↓
           Keycloak 26     ←→    Kafka     →    arda-migration-worker
```

- **Backend:** Java 21 · Spring Boot 3.5 · Spring Security · Liquibase
- **Frontend:** React 19 · TypeScript · Rspack/Rsbuild · Module Federation · Turborepo
- **Security:** APISIX Gateway AuthN (openid-connect) + Internal JWT (RS256)
- **Multi-tenancy:** Separate PostgreSQL database per tenant · Event-driven local config cache (Caffeine + Kafka)
- **Identity:** Keycloak 26 (per-tenant realm)
- **Messaging:** Apache Kafka (KRaft mode, no Zookeeper)
- **Gateway:** Apache APISIX 3.14

## � Danh sách Repositories

### Backend Services

| Repo                       | Port | Chức năng                                               |
| :------------------------- | :--- | :------------------------------------------------------ |
| `arda-shared-kernel`       | lib  | Thư viện lõi: Multi-tenancy, Security, Events           |
| `arda-central-platform`    | 8080 | Quản lý tenant, phát sinh sự kiện tenant lifecycle      |
| `arda-iam-service`         | 8083 | RBAC — Users, Roles, Permissions, Groups (Keycloak + DB)|
| `arda-crm-service`         | 8084 | Quản lý khách hàng, leads, deals                        |
| `arda-bpm-engine`          | 8085 | Workflow và approval engine                             |
| `arda-analysis-service`    | 8086 | BI, Dashboard & Reporting                               |
| `arda-notification`        | 8090 | Push/email notification service                         |
| `arda-migration-worker`    | 8095 | Async provisioning: PostgreSQL DB + Keycloak realm      |

### Frontend (Turborepo Monorepo — `arda-mfe`)

| App              | Port | Chức năng                                                        |
| :--------------- | :--- | :--------------------------------------------------------------- |
| `apps/shell`     | 3000 | Host App — Auth, Tenant Selection, Layout, Navigation            |
| `apps/iam`       | 3001 | MFE — Quản lý người dùng, vai trò, phân quyền                    |
| `apps/bpm`       | 3002 | MFE — Quản lý quy trình nghiệp vụ                                |
| `apps/crm`       | 3003 | MFE — Quản lý khách hàng                                         |

### Infrastructure (`arda-infra-config`)

| Container               | Port(s)    | Vai trò                            |
| :---------------------- | :--------- | :--------------------------------- |
| `arda-postgres`         | 5432       | PostgreSQL 16 — Central + tenant   |
| `arda-keycloak`         | 8081       | Keycloak 26 — Identity per tenant  |
| `arda-apisix`           | 9080, 9180 | API Gateway + Admin API            |
| `arda-kafka`            | 9092       | Event streaming (KRaft)            |
| `arda-kafka-ui`         | 8082       | Kafka management UI                |

## 🔐 Luồng bảo mật

```
1. Browser gửi request → APISIX
2. APISIX [openid-connect] xác thực Keycloak JWT
3. APISIX [internal-jwt-signer.lua] ký Internal JWT (RS256) với claims: sub, tid, roles
4. Microservices nhận X-Internal-Token, xác thực bằng public key (InternalJwtFilter)
5. TenantContext được set → TenantRoutingDataSource route tới đúng tenant DB
```

## 🔄 Luồng cấp phát Tenant

```
Admin tạo tenant (POST /v1/tenants)
  → Central Platform lưu DB
  → Publish: TENANT_CREATED event (Kafka: tenant-events)
  → arda-migration-worker nhận event:
      ├─ Tạo PostgreSQL database + role
      ├─ Chạy Liquibase migrations
      └─ Tạo Keycloak realm + client + default roles
  → Publish: TenantConfigEvent (Kafka: arda.tenant-config-events)
  → Tất cả services cập nhật local cache (zero-latency)
```

## 🛠 Hướng dẫn khởi động nhanh

### 1. Khởi động Infrastructure

```bash
cd arda-infra-config/docker-compose
docker compose up -d
```

### 2. Build Shared Kernel

```bash
cd arda-shared-kernel
./mvnw clean install -DskipTests
```

### 3. Tạo RSA Keypair cho Internal JWT

```powershell
./arda-infra-config/scripts/generate-jwt-keypair.ps1
```

### 4. Cấu hình APISIX Routes

```powershell
./arda-infra-config/scripts/setup-apisix.ps1
```

### 5. Khởi động Frontend

```bash
cd arda-mfe
pnpm install
pnpm dev
```

---

### 🌐 Kết nối với chúng tôi

- 🌍 Website: **[https://arda.io.vn](https://arda.io.vn)**
- 📧 Liên hệ: **contact@arda.io.vn**

---

> 🚀 _Empowering intelligence through data-driven systems._
