# 🧠 Arda Labs

> **Where data flows with intelligence.**

**Arda Labs** là tổ chức công nghệ tiên phong trong:

- Hệ thống **quản lý dữ liệu** và **báo cáo thông minh**
- Ứng dụng **AI** và **phân tích thống kê chuyên sâu**
- Xây dựng **giải pháp microservice hiện đại** và mở rộng linh hoạt

---

### 🧩 Thông tin nhận diện thương hiệu

| Thành phần      | Nội dung                                             |
| --------------- | ---------------------------------------------------- |
| **Logo name**   | `ARDA Labs`                                          |
| **Font chính**  | Space Grotesk (logo), Inter (text)                   |
| **Màu chủ đạo** | Cyan `#06B6D4`, Indigo `#6366F1`, Midnight `#0F172A` |
| **Phong cách**  | Minimal · Futuristic · Data-oriented                 |
| **Slogan**      | _“Where data flows with intelligence.”_              |

---

# Arda Platform - Multi-tenant Enterprise System

Hệ thống quản trị doanh nghiệp đa nền tảng, hỗ trợ Multi-tenancy (Separate Database) chạy trên MicroK8s.

## 🏗 Kiến trúc hệ thống

- **Backend:** Java 21, Spring Boot 3.4, Liquibase.
- **Frontend:** Angular 21, Micro Frontend (Native Federation), PrimeNG + Tailwind v4.
- **Infrastructure:** PostgreSQL (Central), Oracle XE (Tenant), Keycloak, APISIX Gateway.

## 🛰 Quy hoạch Port & Repo

### Backend (Dải 80xx)

| Repo                    | Port | Chức năng                          |
| :---------------------- | :--- | :--------------------------------- |
| `arda-shared-kernel`    | Lib  | Thư viện lõi, Multi-tenant routing |
| `arda-central-platform` | 8000 | Master data, Tenant management     |
| `arda-iam-service`      | 8001 | RBAC, User & Role (Tenant DB)      |
| `arda-analysis-service` | 8009 | BI, Reporting                      |
| `arda-bpm-engine`       | 8010 | Workflow, Approvals                |
| `arda-crm-service`      | 8011 | Leads, Deals, Sales                |

### Frontend (Dải 42xx)

| Repo               | Port | Chức năng                        |
| :----------------- | :--- | :------------------------------- |
| `arda-fe-shell`    | 4200 | Host App, Auth, Layout           |
| `arda-fe-iam`      | 4201 | MFE - Quản lý người dùng, common |
| `arda-fe-analysis` | 4209 | MFE - Dashboard & Reports        |
| `arda-fe-bpm`      | 4210 | MFE - Quản lý quy trình          |
| `arda-fe-crm`      | 4211 | MFE - Quản lý khách hàng         |

## 🛠 Hướng dẫn khởi động nhanh

1. `cd arda-infra-config/docker-compose && docker compose up -d`
2. `cd arda-shared-kernel && ./mvnw clean install`
3. Chạy từng Service Backend/Frontend theo Port quy định.

---

### 🌐 Kết nối với chúng tôi

- Website: **[https://arda.io.vn](https://arda.io.vn)**
- Liên hệ: **contact@arda.io.vn**

---

> 🚀 _Empowering intelligence through data-driven systems._
