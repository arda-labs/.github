# Arda Labs

> Where data flows with intelligence.

**Arda Labs** builds a cloud-native, multi-tenant financial operations platform. The system is organized as independent Git repositories: backend Go microservices, a frontend React Module Federation shell, and GitOps-managed Kubernetes infrastructure.

---

## System Architecture Overview

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1100 720" font-family="'Inter', 'Segoe UI', system-ui, sans-serif">
  <defs>
    <linearGradient id="bgGrad" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0F172A"/>
      <stop offset="100%" stop-color="#1E293B"/>
    </linearGradient>
    <linearGradient id="cyanGrad" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#06B6D4"/>
      <stop offset="100%" stop-color="#0891B2"/>
    </linearGradient>
    <linearGradient id="indigoGrad" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#6366F1"/>
      <stop offset="100%" stop-color="#4F46E5"/>
    </linearGradient>
    <linearGradient id="emeraldGrad" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#10B981"/>
      <stop offset="100%" stop-color="#059669"/>
    </linearGradient>
    <linearGradient id="amberGrad" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#F59E0B"/>
      <stop offset="100%" stop-color="#D97706"/>
    </linearGradient>
    <filter id="glow">
      <feGaussianBlur stdDeviation="3" result="coloredBlur"/>
      <feMerge>
        <feMergeNode in="coloredBlur"/>
        <feMergeNode in="SourceGraphic"/>
      </feMerge>
    </filter>
    <filter id="softShadow">
      <feDropShadow dx="0" dy="2" stdDeviation="4" flood-color="#000" flood-opacity="0.3"/>
    </filter>
    <marker id="arrowCyan" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <path d="M0,0 L8,3 L0,6 Z" fill="#06B6D4"/>
    </marker>
    <marker id="arrowIndigo" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <path d="M0,0 L8,3 L0,6 Z" fill="#6366F1"/>
    </marker>
    <marker id="arrowGray" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <path d="M0,0 L8,3 L0,6 Z" fill="#64748B"/>
    </marker>
  </defs>

  <!-- Background -->
  <rect width="1100" height="720" fill="url(#bgGrad)" rx="12"/>

  <!-- Title -->
  <text x="550" y="36" text-anchor="middle" fill="#E2E8F0" font-size="18" font-weight="700" letter-spacing="1">ARDA PLATFORM — SYSTEM ARCHITECTURE</text>

  <!-- ==================== LAYER 1: CLIENTS ==================== -->
  <rect x="30" y="55" width="1040" height="80" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1" opacity="0.9"/>
  <text x="50" y="78" fill="#64748B" font-size="10" font-weight="600" letter-spacing="2" text-transform="uppercase">CLIENTS</text>

  <!-- Browser -->
  <rect x="60" y="88" width="140" height="36" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1.5"/>
  <text x="130" y="110" text-anchor="middle" fill="#E2E8F0" font-size="12" font-weight="600">🌐 Browser</text>

  <!-- Mobile -->
  <rect x="230" y="88" width="140" height="36" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1.5"/>
  <text x="300" y="110" text-anchor="middle" fill="#E2E8F0" font-size="12" font-weight="600">📱 Mobile App</text>

  <!-- API Client -->
  <rect x="400" y="88" width="140" height="36" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1.5"/>
  <text x="470" y="110" text-anchor="middle" fill="#E2E8F0" font-size="12" font-weight="600">🔌 API Client</text>

  <!-- Arrow: Clients → Cloudflare -->
  <line x1="540" y1="106" x2="620" y2="106" stroke="#64748B" stroke-width="1.5" marker-end="url(#arrowGray)" stroke-dasharray="4,3"/>

  <!-- Cloudflare -->
  <rect x="625" y="85" width="200" height="42" rx="21" fill="url(#amberGrad)" filter="url(#softShadow)"/>
  <text x="725" y="110" text-anchor="middle" fill="#fff" font-size="12" font-weight="700">Cloudflare</text>

  <!-- Arrow: Cloudflare → Tunnel -->
  <line x1="825" y1="106" x2="890" y2="106" stroke="#64748B" stroke-width="1.5" marker-end="url(#arrowGray)"/>

  <!-- Tunnel -->
  <rect x="895" y="85" width="155" height="42" rx="6" fill="#0F172A" stroke="#F59E0B" stroke-width="1.5"/>
  <text x="972" y="110" text-anchor="middle" fill="#FBBF24" font-size="11" font-weight="600">cloudflared Tunnel</text>

  <!-- Arrow: Tunnel → Cluster -->
  <line x1="550" y1="135" x2="550" y2="175" stroke="#64748B" stroke-width="1.5" marker-end="url(#arrowGray)"/>

  <!-- ==================== LAYER 2: CLUSTER ==================== -->
  <rect x="30" y="180" width="1040" height="200" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1" opacity="0.9"/>
  <text x="50" y="202" fill="#64748B" font-size="10" font-weight="600" letter-spacing="2">K3S CLUSTER — INGRESS &amp; AUTH</text>

  <!-- Traefik -->
  <rect x="60" y="212" width="160" height="48" rx="8" fill="#0F172A" stroke="#475569" stroke-width="1.5"/>
  <text x="140" y="231" text-anchor="middle" fill="#E2E8F0" font-size="12" font-weight="600">Traefik Ingress</text>
  <text x="140" y="248" text-anchor="middle" fill="#94A3B8" font-size="9">Reverse Proxy</text>

  <!-- Arrow: Traefik → auth-gateway -->
  <line x1="220" y1="236" x2="290" y2="236" stroke="#64748B" stroke-width="1.5" marker-end="url(#arrowGray)"/>

  <!-- auth-gateway -->
  <rect x="295" y="212" width="180" height="48" rx="8" fill="#0F172A" stroke="#06B6D4" stroke-width="2" filter="url(#softShadow)"/>
  <text x="385" y="231" text-anchor="middle" fill="#06B6D4" font-size="12" font-weight="700">auth-gateway</text>
  <text x="385" y="248" text-anchor="middle" fill="#94A3B8" font-size="9">BFF · Session · ForwardAuth</text>

  <!-- Arrow: auth-gateway → Ory -->
  <line x1="385" y1="260" x2="385" y2="290" stroke="#06B6D4" stroke-width="1" marker-end="url(#arrowCyan)" stroke-dasharray="3,3"/>

  <!-- Ory -->
  <rect x="295" y="295" width="180" height="75" rx="8" fill="#0F172A" stroke="#F59E0B" stroke-width="1.5"/>
  <text x="385" y="314" text-anchor="middle" fill="#FBBF24" font-size="11" font-weight="600">Ory Auth Stack</text>
  <text x="385" y="332" text-anchor="middle" fill="#94A3B8" font-size="9">Hydra (OAuth2/OIDC)</text>
  <text x="385" y="348" text-anchor="middle" fill="#94A3B8" font-size="9">Kratos (Identity)</text>
  <text x="385" y="364" text-anchor="middle" fill="#94A3B8" font-size="9">Permission</text>

  <!-- Arrow: auth-gateway → Services -->
  <line x1="475" y1="236" x2="550" y2="236" stroke="#6366F1" stroke-width="2" marker-end="url(#arrowIndigo)"/>

  <!-- Service label -->
  <text x="512" y="224" text-anchor="middle" fill="#818CF8" font-size="8" font-weight="600">/api/*</text>

  <!-- HTTP/gRPC label -->
  <line x1="550" y1="180" x2="550" y2="212" stroke="#475569" stroke-width="1"/>
  <line x1="850" y1="180" x2="850" y2="212" stroke="#475569" stroke-width="1"/>
  <text x="700" y="206" text-anchor="middle" fill="#475569" font-size="9" font-weight="600">HTTP/JSON · gRPC</text>

  <!-- ==================== LAYER 3: SERVICES ==================== -->
  <rect x="30" y="390" width="1040" height="155" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1" opacity="0.9"/>
  <text x="50" y="412" fill="#64748B" font-size="10" font-weight="600" letter-spacing="2">BACKEND MICROSERVICES</text>

  <!-- Service boxes in a row -->
  <rect x="55" y="422" width="108" height="52" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="109" y="442" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">iam-service</text>
  <text x="109" y="458" text-anchor="middle" fill="#64748B" font-size="8">Identity · RBAC</text>

  <rect x="175" y="422" width="108" height="52" rx="6" fill="#0F172A" stroke="#06B6D4" stroke-width="1.5"/>
  <text x="229" y="442" text-anchor="middle" fill="#67E8F9" font-size="10" font-weight="600">platform-service</text>
  <text x="229" y="458" text-anchor="middle" fill="#64748B" font-size="8">Master Data</text>

  <rect x="295" y="422" width="108" height="52" rx="6" fill="#0F172A" stroke="#10B981" stroke-width="1.5"/>
  <text x="349" y="442" text-anchor="middle" fill="#6EE7B7" font-size="10" font-weight="600">finance-service</text>
  <text x="349" y="458" text-anchor="middle" fill="#64748B" font-size="8">Transactions</text>

  <rect x="415" y="422" width="108" height="52" rx="6" fill="#0F172A" stroke="#F59E0B" stroke-width="1.5"/>
  <text x="469" y="442" text-anchor="middle" fill="#FDE68A" font-size="10" font-weight="600">workflow-service</text>
  <text x="469" y="458" text-anchor="middle" fill="#64748B" font-size="8">Zeebe Facade</text>

  <rect x="535" y="422" width="108" height="52" rx="6" fill="#0F172A" stroke="#EC4899" stroke-width="1.5"/>
  <text x="589" y="442" text-anchor="middle" fill="#F9A8D4" font-size="10" font-weight="600">crm-service</text>
  <text x="589" y="458" text-anchor="middle" fill="#64748B" font-size="8">CRM</text>

  <rect x="655" y="422" width="108" height="52" rx="6" fill="#0F172A" stroke="#8B5CF6" stroke-width="1.5"/>
  <text x="709" y="442" text-anchor="middle" fill="#C4B5FD" font-size="10" font-weight="600">hrm-service</text>
  <text x="709" y="458" text-anchor="middle" fill="#64748B" font-size="8">HRM</text>

  <rect x="775" y="422" width="108" height="52" rx="6" fill="#0F172A" stroke="#14B8A6" stroke-width="1.5"/>
  <text x="829" y="442" text-anchor="middle" fill="#5EEAD4" font-size="10" font-weight="600">notification-svc</text>
  <text x="829" y="458" text-anchor="middle" fill="#64748B" font-size="8">Notifications</text>

  <rect x="895" y="422" width="108" height="52" rx="6" fill="#0F172A" stroke="#F97316" stroke-width="1.5"/>
  <text x="949" y="442" text-anchor="middle" fill="#FDBA74" font-size="10" font-weight="600">media-service</text>
  <text x="949" y="458" text-anchor="middle" fill="#64748B" font-size="8">S3 Storage</text>

  <!-- mdm-service below -->
  <rect x="55" y="482" width="108" height="42" rx="6" fill="#0F172A" stroke="#334155" stroke-width="1" stroke-dasharray="4,3"/>
  <text x="109" y="500" text-anchor="middle" fill="#64748B" font-size="9" font-style="italic">mdm-service</text>
  <text x="109" y="515" text-anchor="middle" fill="#475569" font-size="8">(scaffold)</text>

  <!-- NATS label -->
  <rect x="400" y="482" width="200" height="42" rx="6" fill="#0F172A" stroke="#06B6D4" stroke-width="1.5" stroke-dasharray="4,3"/>
  <text x="500" y="501" text-anchor="middle" fill="#22D3EE" font-size="11" font-weight="600">📨 NATS Event Bus</text>
  <text x="500" y="517" text-anchor="middle" fill="#64748B" font-size="8">Async Events · Outbox Pattern</text>

  <!-- Arrow: services → DB -->
  <line x1="550" y1="545" x2="550" y2="580" stroke="#64748B" stroke-width="1.5" marker-end="url(#arrowGray)"/>

  <!-- ==================== LAYER 4: DATA ==================== -->
  <rect x="30" y="560" width="1040" height="145" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1" opacity="0.9"/>
  <text x="50" y="582" fill="#64748B" font-size="10" font-weight="600" letter-spacing="2">DATA &amp; INFRASTRUCTURE</text>

  <!-- CNPG -->
  <rect x="60" y="592" width="250" height="48" rx="8" fill="#0F172A" stroke="#10B981" stroke-width="1.5"/>
  <text x="185" y="611" text-anchor="middle" fill="#6EE7B7" font-size="11" font-weight="600">CloudNativePG (PostgreSQL 18)</text>
  <text x="185" y="628" text-anchor="middle" fill="#64748B" font-size="9">3-node HA Cluster · 8 databases</text>

  <!-- Valkey -->
  <rect x="325" y="592" width="140" height="48" rx="8" fill="#0F172A" stroke="#F59E0B" stroke-width="1.5"/>
  <text x="395" y="611" text-anchor="middle" fill="#FDE68A" font-size="11" font-weight="600">Valkey</text>
  <text x="395" y="628" text-anchor="middle" fill="#64748B" font-size="9">3-node Cache</text>

  <!-- Garage -->
  <rect x="480" y="592" width="140" height="48" rx="8" fill="#0F172A" stroke="#EC4899" stroke-width="1.5"/>
  <text x="550" y="611" text-anchor="middle" fill="#F9A8D4" font-size="11" font-weight="600">Garage</text>
  <text x="550" y="628" text-anchor="middle" fill="#64748B" font-size="9">3-node S3</text>

  <!-- Zeebe -->
  <rect x="635" y="592" width="140" height="48" rx="8" fill="#0F172A" stroke="#8B5CF6" stroke-width="1.5"/>
  <text x="705" y="611" text-anchor="middle" fill="#C4B5FD" font-size="11" font-weight="600">Zeebe 8.5</text>
  <text x="705" y="628" text-anchor="middle" fill="#64748B" font-size="9">BPMN Engine</text>

  <!-- ArgoCD -->
  <rect x="790" y="592" width="150" height="48" rx="8" fill="#0F172A" stroke="#06B6D4" stroke-width="1.5"/>
  <text x="865" y="611" text-anchor="middle" fill="#22D3EE" font-size="11" font-weight="600">Argo CD</text>
  <text x="865" y="628" text-anchor="middle" fill="#64748B" font-size="9">GitOps · Image Updater</text>

  <!-- Bottom note -->
  <text x="550" y="680" text-anchor="middle" fill="#475569" font-size="10">
    MFE Frontend · Traefik Ingress · Auth Gateway · 9 Backend Services · PostgreSQL · NATS · Valkey · Garage S3 · Zeebe · Argo CD
  </text>
</svg>
```
---

## Service Topology & Communication

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1100 650" font-family="'Inter', 'Segoe UI', system-ui, sans-serif">
  <defs>
    <linearGradient id="bgGrad2" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0F172A"/>
      <stop offset="100%" stop-color="#1E293B"/>
    </linearGradient>
    <filter id="shadow2">
      <feDropShadow dx="0" dy="2" stdDeviation="3" flood-color="#000" flood-opacity="0.3"/>
    </filter>
    <marker id="arrCyan" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <path d="M0,0 L8,3 L0,6 Z" fill="#06B6D4"/>
    </marker>
    <marker id="arrGreen" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <path d="M0,0 L8,3 L0,6 Z" fill="#10B981"/>
    </marker>
    <marker id="arrPurple" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <path d="M0,0 L8,3 L0,6 Z" fill="#8B5CF6"/>
    </marker>
  </defs>

  <rect width="1100" height="650" fill="url(#bgGrad2)" rx="12"/>

  <text x="550" y="36" text-anchor="middle" fill="#E2E8F0" font-size="18" font-weight="700" letter-spacing="1">SERVICE TOPOLOGY — COMMUNICATION PATTERNS</text>

  <!-- Legend -->
  <rect x="30" y="52" width="300" height="70" rx="6" fill="#1E293B" stroke="#334155" stroke-width="1"/>
  <text x="44" y="70" fill="#94A3B8" font-size="9" font-weight="600">LEGEND</text>
  <line x1="44" y1="88" x2="90" y2="88" stroke="#06B6D4" stroke-width="2" marker-end="url(#arrCyan)"/>
  <text x="96" y="92" fill="#94A3B8" font-size="10">HTTP/JSON (API calls)</text>
  <line x1="44" y1="108" x2="90" y2="108" stroke="#8B5CF6" stroke-width="2" marker-end="url(#arrPurple)"/>
  <text x="96" y="112" fill="#94A3B8" font-size="10">gRPC (service-to-service)</text>
  <line x1="220" y1="88" x2="266" y2="88" stroke="#10B981" stroke-width="2" marker-end="url(#arrGreen)" stroke-dasharray="4,3"/>
  <text x="272" y="92" fill="#94A3B8" font-size="10">NATS Events (async)</text>

  <!-- FRONTEND SECTION -->
  <rect x="30" y="130" width="450" height="240" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1" opacity="0.8"/>
  <text x="44" y="152" fill="#64748B" font-size="10" font-weight="600" letter-spacing="1">FRONTEND — MODULE FEDERATION</text>

  <!-- Shell -->
  <rect x="44" y="162" width="130" height="50" rx="8" fill="#0F172A" stroke="#06B6D4" stroke-width="2" filter="url(#shadow2)"/>
  <text x="109" y="181" text-anchor="middle" fill="#22D3EE" font-size="12" font-weight="700">Shell</text>
  <text x="109" y="198" text-anchor="middle" fill="#64748B" font-size="9">Layout · Auth · Nav</text>

  <!-- Remotes column -->
  <rect x="210" y="162" width="100" height="50" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="260" y="182" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">mfe-iam</text>
  <text x="260" y="198" text-anchor="middle" fill="#64748B" font-size="8">5101</text>

  <rect x="210" y="220" width="100" height="50" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="260" y="240" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">mfe-platform</text>
  <text x="260" y="256" text-anchor="middle" fill="#64748B" font-size="8">5102</text>

  <rect x="210" y="278" width="100" height="50" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="260" y="298" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">mfe-finance</text>
  <text x="260" y="314" text-anchor="middle" fill="#64748B" font-size="8">5103</text>

  <!-- Remotes column 2 -->
  <rect x="325" y="162" width="100" height="50" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="375" y="182" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">mfe-account</text>
  <text x="375" y="198" text-anchor="middle" fill="#64748B" font-size="8">5104</text>

  <rect x="325" y="220" width="100" height="50" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="375" y="240" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">mfe-hrm</text>
  <text x="375" y="256" text-anchor="middle" fill="#64748B" font-size="8">5105</text>

  <rect x="325" y="278" width="100" height="50" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="375" y="298" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">mfe-workflow</text>
  <text x="375" y="314" text-anchor="middle" fill="#64748B" font-size="8">5106</text>

  <!-- Remotes row 3 -->
  <rect x="210" y="336" width="215" height="24" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="317" y="353" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">mfe-crm (5107)</text>

  <!-- Arrow from shell to remotes -->
  <text x="180" y="190" fill="#475569" font-size="8">→</text>

  <!-- BACKEND SECTION -->
  <rect x="500" y="130" width="570" height="340" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1" opacity="0.8"/>
  <text x="514" y="152" fill="#64748B" font-size="10" font-weight="600" letter-spacing="1">BACKEND — MICROSERVICES</text>

  <!-- auth-gateway top -->
  <rect x="514" y="165" width="220" height="42" rx="8" fill="#0F172A" stroke="#06B6D4" stroke-width="2" filter="url(#shadow2)"/>
  <text x="624" y="185" text-anchor="middle" fill="#22D3EE" font-size="12" font-weight="700">auth-gateway :8082</text>
  <text x="624" y="199" text-anchor="middle" fill="#64748B" font-size="8">BFF · Session · ForwardAuth · Policy</text>

  <!-- Arrow from frontend to auth-gateway -->
  <line x1="480" y1="185" x2="505" y2="185" stroke="#06B6D4" stroke-width="2" marker-end="url(#arrCyan)"/>

  <!-- Services grid 3x3 -->
  <!-- Row 1 -->
  <rect x="514" y="220" width="170" height="42" rx="6" fill="#0F172A" stroke="#6366F1" stroke-width="1.5"/>
  <text x="599" y="238" text-anchor="middle" fill="#A5B4FC" font-size="10" font-weight="600">iam-service :8081</text>
  <text x="599" y="254" text-anchor="middle" fill="#64748B" font-size="8">Identity · RBAC · MFA</text>

  <rect x="695" y="220" width="170" height="42" rx="6" fill="#0F172A" stroke="#06B6D4" stroke-width="1.5"/>
  <text x="780" y="238" text-anchor="middle" fill="#67E8F9" font-size="10" font-weight="600">platform-service :8091</text>
  <text x="780" y="254" text-anchor="middle" fill="#64748B" font-size="8">Master Data · Lookups</text>

  <rect x="876" y="220" width="180" height="42" rx="6" fill="#0F172A" stroke="#10B981" stroke-width="1.5"/>
  <text x="966" y="238" text-anchor="middle" fill="#6EE7B7" font-size="10" font-weight="600">finance-service :8090</text>
  <text x="966" y="254" text-anchor="middle" fill="#64748B" font-size="8">Accounts · Transactions</text>

  <!-- Row 2 -->
  <rect x="514" y="270" width="170" height="42" rx="6" fill="#0F172A" stroke="#F59E0B" stroke-width="1.5"/>
  <text x="599" y="288" text-anchor="middle" fill="#FDE68A" font-size="10" font-weight="600">workflow-service :8093</text>
  <text x="599" y="304" text-anchor="middle" fill="#64748B" font-size="8">Zeebe Facade · Cases</text>

  <rect x="695" y="270" width="170" height="42" rx="6" fill="#0F172A" stroke="#EC4899" stroke-width="1.5"/>
  <text x="780" y="288" text-anchor="middle" fill="#F9A8D4" font-size="10" font-weight="600">crm-service :8094</text>
  <text x="780" y="304" text-anchor="middle" fill="#64748B" font-size="8">Customers · Workbench</text>

  <rect x="876" y="270" width="180" height="42" rx="6" fill="#0F172A" stroke="#8B5CF6" stroke-width="1.5"/>
  <text x="966" y="288" text-anchor="middle" fill="#C4B5FD" font-size="10" font-weight="600">hrm-service :8097</text>
  <text x="966" y="304" text-anchor="middle" fill="#64748B" font-size="8">Employees · Org Units</text>

  <!-- Row 3 -->
  <rect x="514" y="320" width="170" height="42" rx="6" fill="#0F172A" stroke="#14B8A6" stroke-width="1.5"/>
  <text x="599" y="338" text-anchor="middle" fill="#5EEAD4" font-size="10" font-weight="600">notification-svc :8095</text>
  <text x="599" y="354" text-anchor="middle" fill="#64748B" font-size="8">Notifications · Push</text>

  <rect x="695" y="320" width="170" height="42" rx="6" fill="#0F172A" stroke="#F97316" stroke-width="1.5"/>
  <text x="780" y="338" text-anchor="middle" fill="#FDBA74" font-size="10" font-weight="600">media-service :8092</text>
  <text x="780" y="354" text-anchor="middle" fill="#64748B" font-size="8">S3 · Garage Storage</text>

  <rect x="876" y="320" width="180" height="42" rx="6" fill="#0F172A" stroke="#334155" stroke-width="1" stroke-dasharray="4,3"/>
  <text x="966" y="338" text-anchor="middle" fill="#64748B" font-size="9" font-style="italic">mdm-service :8096</text>
  <text x="966" y="354" text-anchor="middle" fill="#475569" font-size="8">(scaffold)</text>

  <!-- gRPC arrows between services -->
  <line x1="770" y1="240" x2="770" y2="260" stroke="#8B5CF6" stroke-width="1.5" marker-end="url(#arrPurple)" stroke-dasharray="3,2"/>
  <line x1="624" y1="261" x2="624" y2="286" stroke="#8B5CF6" stroke-width="1.5" marker-end="url(#arrPurple)" stroke-dasharray="3,2"/>
  <line x1="780" y1="311" x2="780" y2="336" stroke="#8B5CF6" stroke-width="1.5" marker-end="url(#arrPurple)" stroke-dasharray="3,2"/>

  <!-- NATS bus -->
  <rect x="514" y="375" width="542" height="32" rx="6" fill="#0F172A" stroke="#06B6D4" stroke-width="1.5" stroke-dasharray="4,3"/>
  <text x="785" y="395" text-anchor="middle" fill="#22D3EE" font-size="10" font-weight="600">📨 NATS Event Bus — JetStream — Transactional Outbox</text>

  <!-- Services connect to NATS -->
  <line x1="580" y1="362" x2="580" y2="370" stroke="#10B981" stroke-width="1" marker-end="url(#arrGreen)" stroke-dasharray="3,2"/>
  <line x1="750" y1="362" x2="750" y2="370" stroke="#10B981" stroke-width="1" marker-end="url(#arrGreen)" stroke-dasharray="3,2"/>
  <line x1="950" y1="362" x2="950" y2="370" stroke="#10B981" stroke-width="1" marker-end="url(#arrGreen)" stroke-dasharray="3,2"/>

  <!-- DATA SECTION -->
  <rect x="30" y="380" width="450" height="95" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1" opacity="0.8"/>
  <text x="44" y="400" fill="#64748B" font-size="10" font-weight="600" letter-spacing="1">SHARED PACKAGES</text>

  <rect x="44" y="410" width="125" height="24" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1"/>
  <text x="106" y="427" text-anchor="middle" fill="#94A3B8" font-size="9">@workspace/ui</text>
  <rect x="178" y="410" width="125" height="24" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1"/>
  <text x="240" y="427" text-anchor="middle" fill="#94A3B8" font-size="9">@workspace/api</text>
  <rect x="312" y="410" width="125" height="24" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1"/>
  <text x="374" y="427" text-anchor="middle" fill="#94A3B8" font-size="9">@workspace/auth</text>
  <rect x="44" y="442" width="125" height="24" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1"/>
  <text x="106" y="459" text-anchor="middle" fill="#94A3B8" font-size="9">@workspace/i18n</text>
  <rect x="178" y="442" width="125" height="24" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1"/>
  <text x="240" y="459" text-anchor="middle" fill="#94A3B8" font-size="9">@workspace/theme</text>
  <rect x="312" y="442" width="125" height="24" rx="6" fill="#0F172A" stroke="#475569" stroke-width="1"/>
  <text x="374" y="459" text-anchor="middle" fill="#94A3B8" font-size="9">@workspace/core</text>

  <!-- DATABASES -->
  <rect x="30" y="485" width="1040" height="150" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1" opacity="0.8"/>
  <text x="44" y="505" fill="#64748B" font-size="10" font-weight="600" letter-spacing="1">DATABASES &amp; INFRASTRUCTURE</text>

  <!-- CNPG cluster -->
  <rect x="44" y="515" width="700" height="55" rx="8" fill="#0F172A" stroke="#10B981" stroke-width="1.5"/>
  <text x="60" y="535" fill="#6EE7B7" font-size="11" font-weight="600">CloudNativePG Cluster (pg-main) — PostgreSQL 18</text>

  <!-- DBs in a row -->
  <rect x="50" y="545" width="72" height="20" rx="4" fill="#064E3B" stroke="#10B981" stroke-width="0.5"/>
  <text x="86" y="559" text-anchor="middle" fill="#6EE7B7" font-size="8">iam</text>
  <rect x="128" y="545" width="72" height="20" rx="4" fill="#064E3B" stroke="#10B981" stroke-width="0.5"/>
  <text x="164" y="559" text-anchor="middle" fill="#6EE7B7" font-size="8">common</text>
  <rect x="206" y="545" width="72" height="20" rx="4" fill="#064E3B" stroke="#10B981" stroke-width="0.5"/>
  <text x="242" y="559" text-anchor="middle" fill="#6EE7B7" font-size="8">finance</text>
  <rect x="284" y="545" width="72" height="20" rx="4" fill="#064E3B" stroke="#10B981" stroke-width="0.5"/>
  <text x="320" y="559" text-anchor="middle" fill="#6EE7B7" font-size="8">workflow</text>
  <rect x="362" y="545" width="72" height="20" rx="4" fill="#064E3B" stroke="#10B981" stroke-width="0.5"/>
  <text x="398" y="559" text-anchor="middle" fill="#6EE7B7" font-size="8">crm</text>
  <rect x="440" y="545" width="72" height="20" rx="4" fill="#064E3B" stroke="#10B981" stroke-width="0.5"/>
  <text x="476" y="559" text-anchor="middle" fill="#6EE7B7" font-size="8">hrm</text>
  <rect x="518" y="545" width="72" height="20" rx="4" fill="#064E3B" stroke="#10B981" stroke-width="0.5"/>
  <text x="554" y="559" text-anchor="middle" fill="#6EE7B7" font-size="8">notification</text>
  <rect x="596" y="545" width="72" height="20" rx="4" fill="#064E3B" stroke="#10B981" stroke-width="0.5"/>
  <text x="632" y="559" text-anchor="middle" fill="#6EE7B7" font-size="8">media</text>

  <!-- Infra boxes -->
  <rect x="760" y="515" width="130" height="55" rx="6" fill="#0F172A" stroke="#F59E0B" stroke-width="1.5"/>
  <text x="825" y="535" text-anchor="middle" fill="#FDE68A" font-size="10" font-weight="600">Valkey</text>
  <text x="825" y="552" text-anchor="middle" fill="#64748B" font-size="8">3-node Cache</text>
  <text x="825" y="564" text-anchor="middle" fill="#475569" font-size="7">Redis-compatible</text>

  <rect x="898" y="515" width="130" height="55" rx="6" fill="#0F172A" stroke="#EC4899" stroke-width="1.5"/>
  <text x="963" y="535" text-anchor="middle" fill="#F9A8D4" font-size="10" font-weight="600">Garage</text>
  <text x="963" y="552" text-anchor="middle" fill="#64748B" font-size="8">3-node S3</text>
  <text x="963" y="564" text-anchor="middle" fill="#475569" font-size="7">Object Storage</text>

  <!-- Services → DB arrows -->
  <line x1="624" y1="470" x2="624" y2="510" stroke="#10B981" stroke-width="1" marker-end="url(#arrGreen)" stroke-dasharray="3,2"/>
  <line x1="780" y1="470" x2="780" y2="510" stroke="#10B981" stroke-width="1" marker-end="url(#arrGreen)" stroke-dasharray="3,2"/>
  <line x1="966" y1="470" x2="966" y2="510" stroke="#10B981" stroke-width="1" marker-end="url(#arrGreen)" stroke-dasharray="3,2"/>

  <!-- Bottom labels -->
  <text x="550" y="625" text-anchor="middle" fill="#475569" font-size="9">
    Shared Libraries: arda-auth · arda-errors · arda-events · arda-grpc · arda-http · arda-postgres · arda-redis · arda-proto
  </text>
</svg>
```

---

## Authentication Flow

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1100 520" font-family="'Inter', 'Segoe UI', system-ui, sans-serif">
  <defs>
    <linearGradient id="bgGrad3" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0F172A"/>
      <stop offset="100%" stop-color="#1E293B"/>
    </linearGradient>
    <filter id="shadow3">
      <feDropShadow dx="0" dy="2" stdDeviation="3" flood-color="#000" flood-opacity="0.3"/>
    </filter>
    <marker id="arr3" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <path d="M0,0 L8,3 L0,6 Z" fill="#06B6D4"/>
    </marker>
  </defs>

  <rect width="1100" height="520" fill="url(#bgGrad3)" rx="12"/>

  <text x="550" y="36" text-anchor="middle" fill="#E2E8F0" font-size="18" font-weight="700" letter-spacing="1">AUTHENTICATION &amp; AUTHORIZATION FLOW</text>

  <!-- Components -->
  <!-- Browser -->
  <rect x="60" y="140" width="140" height="50" rx="8" fill="#0F172A" stroke="#475569" stroke-width="1.5" filter="url(#shadow3)"/>
  <text x="130" y="160" text-anchor="middle" fill="#E2E8F0" font-size="12" font-weight="600">🌐 Browser</text>
  <text x="130" y="178" text-anchor="middle" fill="#64748B" font-size="9">User Agent</text>

  <!-- Traefik -->
  <rect x="250" y="140" width="130" height="50" rx="8" fill="#0F172A" stroke="#475569" stroke-width="1.5" filter="url(#shadow3)"/>
  <text x="315" y="160" text-anchor="middle" fill="#E2E8F0" font-size="11" font-weight="600">Traefik</text>
  <text x="315" y="178" text-anchor="middle" fill="#64748B" font-size="9">ForwardAuth</text>

  <!-- auth-gateway -->
  <rect x="430" y="100" width="160" height="60" rx="8" fill="#0F172A" stroke="#06B6D4" stroke-width="2" filter="url(#shadow3)"/>
  <text x="510" y="122" text-anchor="middle" fill="#22D3EE" font-size="12" font-weight="700">auth-gateway</text>
  <text x="510" y="140" text-anchor="middle" fill="#94A3B8" font-size="9">BFF Session</text>
  <text x="510" y="154" text-anchor="middle" fill="#94A3B8" font-size="9">/api/auth/*</text>

  <!-- Kratos -->
  <rect x="640" y="60" width="140" height="50" rx="6" fill="#0F172A" stroke="#F59E0B" stroke-width="1.5" filter="url(#shadow3)"/>
  <text x="710" y="80" text-anchor="middle" fill="#FBBF24" font-size="11" font-weight="600">Ory Kratos</text>
  <text x="710" y="98" text-anchor="middle" fill="#64748B" font-size="9">Identity &amp; Auth</text>

  <!-- Hydra -->
  <rect x="640" y="160" width="140" height="50" rx="6" fill="#0F172A" stroke="#F59E0B" stroke-width="1.5" filter="url(#shadow3)"/>
  <text x="710" y="180" text-anchor="middle" fill="#FBBF24" font-size="11" font-weight="600">Ory Hydra</text>
  <text x="710" y="198" text-anchor="middle" fill="#64748B" font-size="9">OAuth2 / OIDC</text>

  <!-- iam-service -->
  <rect x="430" y="240" width="160" height="50" rx="8" fill="#0F172A" stroke="#6366F1" stroke-width="2" filter="url(#shadow3)"/>
  <text x="510" y="260" text-anchor="middle" fill="#A5B4FC" font-size="12" font-weight="700">iam-service</text>
  <text x="510" y="278" text-anchor="middle" fill="#94A3B8" font-size="9">Users · RBAC · MFA</text>

  <!-- Downstream service -->
  <rect x="690" y="250" width="140" height="50" rx="6" fill="#0F172A" stroke="#10B981" stroke-width="1.5" filter="url(#shadow3)"/>
  <text x="760" y="270" text-anchor="middle" fill="#6EE7B7" font-size="11" font-weight="600">Domain Svc</text>
  <text x="760" y="288" text-anchor="middle" fill="#64748B" font-size="9">Service</text>

  <!-- Flow arrows - Login -->
  <line x1="200" y1="165" x2="240" y2="165" stroke="#06B6D4" stroke-width="2" marker-end="url(#arr3)"/>
  <text x="216" y="156" fill="#0EA5E9" font-size="8">①</text>

  <line x1="380" y1="165" x2="420" y2="143" stroke="#06B6D4" stroke-width="2" marker-end="url(#arr3)"/>
  <text x="393" y="156" fill="#0EA5E9" font-size="8">②</text>

  <line x1="510" y1="100" x2="620" y2="95" stroke="#06B6D4" stroke-width="1.5" marker-end="url(#arr3)"/>
  <text x="560" y="90" fill="#0EA5E9" font-size="8">③ Login API</text>

  <line x1="710" y1="110" x2="510" y2="130" stroke="#06B6D4" stroke-width="1.5" marker-end="url(#arr3)"/>
  <text x="590" y="118" fill="#0EA5E9" font-size="8">④ Validate</text>

  <!-- Hydra flow -->
  <line x1="510" y1="160" x2="620" y2="180" stroke="#6366F1" stroke-width="1.5" marker-end="url(#arr3)"/>
  <text x="558" y="174" fill="#818CF8" font-size="8">Accept Hydra login</text>

  <!-- IAM linking -->
  <line x1="510" y1="200" x2="510" y2="230" stroke="#6366F1" stroke-width="1.5" marker-end="url(#arr3)"/>
  <text x="472" y="218" fill="#818CF8" font-size="8">⑤ Resolve IAM user</text>

  <!-- Session creation -->
  <line x1="510" y1="240" x2="130" y2="195" stroke="#10B981" stroke-width="2" marker-end="url(#arr3)" stroke-dasharray="5,3"/>
  <text x="320" y="210" fill="#10B981" font-size="8">⑥ BFF Session Created</text>

  <!-- Downstream request flow -->
  <line x1="590" y1="265" x2="680" y2="275" stroke="#10B981" stroke-width="1.5" marker-end="url(#arr3)"/>
  <text x="630" y="258" fill="#10B981" font-size="8">X-User-Id, X-Tenant-Id</text>
  <text x="630" y="248" fill="#10B981" font-size="8">X-Roles, X-Permissions</text>

  <!-- Protected request -->
  <path d="M 130 185 L 130 400 L 315 400 L 315 200" fill="none" stroke="#64748B" stroke-width="1.5" marker-end="url(#arr3)" stroke-dasharray="4,3"/>
  <text x="220" y="396" fill="#64748B" font-size="8">Subsequent requests → Cookie/Session</text>

  <!-- Header details box -->
  <rect x="60" y="370" width="480" height="90" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1"/>
  <text x="76" y="390" fill="#94A3B8" font-size="9" font-weight="600">USER CONTEXT HEADERS (injected by auth-gateway to downstream services)</text>
  <text x="76" y="410" fill="#22D3EE" font-size="9">X-User-Id</text>
  <text x="160" y="410" fill="#94A3B8" font-size="9">IAM user UUID — canonical actor key</text>
  <text x="76" y="428" fill="#22D3EE" font-size="9">X-Tenant-Id</text>
  <text x="160" y="428" fill="#94A3B8" font-size="9">Current tenant identifier</text>
  <text x="76" y="446" fill="#22D3EE" font-size="9">X-Roles · X-Permissions</text>
  <text x="226" y="446" fill="#94A3B8" font-size="9">Comma-separated role/permission codes</text>

  <!-- Policy box -->
  <rect x="560" y="370" width="480" height="90" rx="8" fill="#1E293B" stroke="#334155" stroke-width="1"/>
  <text x="576" y="390" fill="#94A3B8" font-size="9" font-weight="600">AUTH POLICY — ROUTE PROTECTION</text>
  <text x="576" y="410" fill="#6EE7B7" font-size="9">GET /api/platform/**</text>
  <text x="750" y="410" fill="#94A3B8" font-size="9">→ platform.read</text>
  <text x="576" y="428" fill="#FBBF24" font-size="9">POST/PUT/DELETE /api/platform/**</text>
  <text x="770" y="428" fill="#94A3B8" font-size="9">→ platform.manage</text>
  <text x="576" y="446" fill="#F87171" font-size="9">POST/PUT/DELETE /api/iam/users/**</text>
  <text x="776" y="446" fill="#94A3B8" font-size="9">→ iam.user.manage (risk: high)</text>

  <!-- Legend -->
  <rect x="60" y="475" width="200" height="24" rx="6" fill="#1E293B" stroke="#334155" stroke-width="1"/>
  <text x="76" y="492" fill="#94A3B8" font-size="9">Flow: Login → Auth → Session → Protected Request</text>
</svg>
```

---

## Infrastructure & GitOps

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1100 580" font-family="'Inter', 'Segoe UI', system-ui, sans-serif">
  <defs>
    <linearGradient id="bgGrad4" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0F172A"/>
      <stop offset="100%" stop-color="#1E293B"/>
    </linearGradient>
    <filter id="shadow4">
      <feDropShadow dx="0" dy="2" stdDeviation="3" flood-color="#000" flood-opacity="0.3"/>
    </filter>
    <marker id="arr4" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
      <path d="M0,0 L8,3 L0,6 Z" fill="#06B6D4"/>
    </marker>
  </defs>

  <rect width="1100" height="580" fill="url(#bgGrad4)" rx="12"/>

  <text x="550" y="36" text-anchor="middle" fill="#E2E8F0" font-size="18" font-weight="700" letter-spacing="1">INFRASTRUCTURE — K3S CLUSTER &amp; GITOPS</text>

  <!-- GitHub -->
  <rect x="60" y="60" width="160" height="55" rx="8" fill="#0F172A" stroke="#475569" stroke-width="1.5" filter="url(#shadow4)"/>
  <text x="140" y="82" text-anchor="middle" fill="#E2E8F0" font-size="12" font-weight="600">GitHub Repos</text>
  <text x="140" y="100" text-anchor="middle" fill="#94A3B8" font-size="9">arda-be · arda-mfe</text>
  <text x="140" y="112" text-anchor="middle" fill="#94A3B8" font-size="9">arda-infra</text>

  <!-- GHCR -->
  <rect x="60" y="130" width="160" height="45" rx="8" fill="#0F172A" stroke="#F59E0B" stroke-width="1" filter="url(#shadow4)"/>
  <text x="140" y="150" text-anchor="middle" fill="#FBBF24" font-size="11" font-weight="600">GHCR</text>
  <text x="140" y="166" text-anchor="middle" fill="#94A3B8" font-size="9">Container Registry</text>

  <!-- Arrow → ArgoCD -->
  <line x1="220" y1="85" x2="330" y2="85" stroke="#06B6D4" stroke-width="2" marker-end="url(#arr4)"/>
  <text x="270" y="76" fill="#0EA5E9" font-size="8">Git push</text>

  <!-- ArgoCD -->
  <rect x="340" y="55" width="200" height="60" rx="8" fill="#0F172A" stroke="#06B6D4" stroke-width="2" filter="url(#shadow4)"/>
  <text x="440" y="77" text-anchor="middle" fill="#22D3EE" font-size="13" font-weight="700">Argo CD</text>
  <text x="440" y="97" text-anchor="middle" fill="#94A3B8" font-size="9">GitOps · Sync · Health Checks</text>
  <text x="440" y="110" text-anchor="middle" fill="#64748B" font-size="8">Image Updater</text>

  <!-- Arrow → Cluster -->
  <line x1="540" y1="85" x2="650" y2="85" stroke="#06B6D4" stroke-width="2" marker-end="url(#arr4)"/>
  <text x="590" y="76" fill="#0EA5E9" font-size="8">Sync</text>

  <!-- ==================== CLUSTER ==================== -->
  <rect x="40" y="200" width="1020" height="365" rx="10" fill="#1E293B" stroke="#334155" stroke-width="2"/>
  <text x="60" y="222" fill="#64748B" font-size="10" font-weight="600" letter-spacing="1">K3S CLUSTER — 3 NODES</text>

  <!-- Node 1 -->
  <rect x="60" y="235" width="310" height="315" rx="8" fill="#0F172A" stroke="#334155" stroke-width="1"/>
  <text x="215" y="255" text-anchor="middle" fill="#E2E8F0" font-size="11" font-weight="600">k3s-node1</text>
  <text x="215" y="270" text-anchor="middle" fill="#64748B" font-size="8">192.168.100.201</text>

  <rect x="75" y="282" width="130" height="35" rx="6" fill="#1E293B" stroke="#06B6D4" stroke-width="1"/>
  <text x="140" y="300" text-anchor="middle" fill="#22D3EE" font-size="9" font-weight="600">control-plane</text>
  <text x="140" y="314" text-anchor="middle" fill="#64748B" font-size="7">etcd</text>

  <rect x="218" y="282" width="130" height="35" rx="6" fill="#1E293B" stroke="#10B981" stroke-width="1"/>
  <text x="283" y="300" text-anchor="middle" fill="#6EE7B7" font-size="9" font-weight="600">PostgreSQL</text>
  <text x="283" y="314" text-anchor="middle" fill="#64748B" font-size="7">CNPG replica</text>

  <rect x="75" y="328" width="130" height="35" rx="6" fill="#1E293B" stroke="#F59E0B" stroke-width="1"/>
  <text x="140" y="346" text-anchor="middle" fill="#FBBF24" font-size="9" font-weight="600">Traefik</text>
  <text x="140" y="360" text-anchor="middle" fill="#64748B" font-size="7">Ingress</text>

  <rect x="218" y="328" width="130" height="35" rx="6" fill="#1E293B" stroke="#6366F1" stroke-width="1"/>
  <text x="283" y="346" text-anchor="middle" fill="#A5B4FC" font-size="9" font-weight="600">App Pods</text>
  <text x="283" y="360" text-anchor="middle" fill="#64748B" font-size="7">Round-robin</text>

  <!-- Node 2 -->
  <rect x="395" y="235" width="310" height="315" rx="8" fill="#0F172A" stroke="#334155" stroke-width="1"/>
  <text x="550" y="255" text-anchor="middle" fill="#E2E8F0" font-size="11" font-weight="600">k3s-node2</text>
  <text x="550" y="270" text-anchor="middle" fill="#64748B" font-size="8">192.168.100.202</text>

  <rect x="410" y="282" width="130" height="35" rx="6" fill="#1E293B" stroke="#06B6D4" stroke-width="1"/>
  <text x="475" y="300" text-anchor="middle" fill="#22D3EE" font-size="9" font-weight="600">control-plane</text>
  <text x="475" y="314" text-anchor="middle" fill="#64748B" font-size="7">etcd</text>

  <rect x="553" y="282" width="130" height="35" rx="6" fill="#1E293B" stroke="#10B981" stroke-width="1"/>
  <text x="618" y="300" text-anchor="middle" fill="#6EE7B7" font-size="9" font-weight="600">PostgreSQL</text>
  <text x="618" y="314" text-anchor="middle" fill="#64748B" font-size="7">CNPG replica</text>

  <rect x="410" y="328" width="130" height="35" rx="6" fill="#1E293B" stroke="#8B5CF6" stroke-width="1"/>
  <text x="475" y="346" text-anchor="middle" fill="#C4B5FD" font-size="9" font-weight="600">NATS</text>
  <text x="475" y="360" text-anchor="middle" fill="#64748B" font-size="7">JetStream</text>

  <rect x="553" y="328" width="130" height="35" rx="6" fill="#1E293B" stroke="#EC4899" stroke-width="1"/>
  <text x="618" y="346" text-anchor="middle" fill="#F9A8D4" font-size="9" font-weight="600">Valkey</text>
  <text x="618" y="360" text-anchor="middle" fill="#64748B" font-size="7">Cache</text>

  <!-- Node 3 -->
  <rect x="730" y="235" width="310" height="315" rx="8" fill="#0F172A" stroke="#334155" stroke-width="1"/>
  <text x="885" y="255" text-anchor="middle" fill="#E2E8F0" font-size="11" font-weight="600">k3s-node3</text>
  <text x="885" y="270" text-anchor="middle" fill="#64748B" font-size="8">192.168.100.203</text>

  <rect x="745" y="282" width="130" height="35" rx="6" fill="#1E293B" stroke="#06B6D4" stroke-width="1"/>
  <text x="810" y="300" text-anchor="middle" fill="#22D3EE" font-size="9" font-weight="600">control-plane</text>
  <text x="810" y="314" text-anchor="middle" fill="#64748B" font-size="7">etcd</text>

  <rect x="888" y="282" width="130" height="35" rx="6" fill="#1E293B" stroke="#10B981" stroke-width="1"/>
  <text x="953" y="300" text-anchor="middle" fill="#6EE7B7" font-size="9" font-weight="600">PostgreSQL</text>
  <text x="953" y="314" text-anchor="middle" fill="#64748B" font-size="7">CNPG replica</text>

  <rect x="745" y="328" width="130" height="35" rx="6" fill="#1E293B" stroke="#14B8A6" stroke-width="1"/>
  <text x="810" y="346" text-anchor="middle" fill="#5EEAD4" font-size="9" font-weight="600">Zeebe</text>
  <text x="810" y="360" text-anchor="middle" fill="#64748B" font-size="7">BPMN Engine</text>

  <rect x="888" y="328" width="130" height="35" rx="6" fill="#1E293B" stroke="#F97316" stroke-width="1"/>
  <text x="953" y="346" text-anchor="middle" fill="#FDBA74" font-size="9" font-weight="600">Garage</text>
  <text x="953" y="360" text-anchor="middle" fill="#64748B" font-size="7">S3 Storage</text>

  <!-- Namespaces section -->
  <text x="60" y="395" fill="#64748B" font-size="9" font-weight="600" letter-spacing="1">NAMESPACES</text>

  <rect x="60" y="405" width="960" height="30" rx="6" fill="#1E293B" stroke="#475569" stroke-width="1"/>
  <rect x="65" y="409" width="80" height="22" rx="4" fill="#0F172A" stroke="#06B6D4" stroke-width="0.5"/>
  <text x="105" y="424" text-anchor="middle" fill="#22D3EE" font-size="8">auth</text>
  <rect x="150" y="409" width="80" height="22" rx="4" fill="#0F172A" stroke="#10B981" stroke-width="0.5"/>
  <text x="190" y="424" text-anchor="middle" fill="#6EE7B7" font-size="8">database</text>
  <rect x="235" y="409" width="80" height="22" rx="4" fill="#0F172A" stroke="#F59E0B" stroke-width="0.5"/>
  <text x="275" y="424" text-anchor="middle" fill="#FBBF24" font-size="8">platform</text>
  <rect x="320" y="409" width="80" height="22" rx="4" fill="#0F172A" stroke="#6366F1" stroke-width="0.5"/>
  <text x="360" y="424" text-anchor="middle" fill="#A5B4FC" font-size="8">arda-app</text>
  <rect x="405" y="409" width="80" height="22" rx="4" fill="#0F172A" stroke="#EC4899" stroke-width="0.5"/>
  <text x="445" y="424" text-anchor="middle" fill="#F9A8D4" font-size="8">arda-web</text>
  <text x="510" y="424" fill="#475569" font-size="8">and more...</text>

  <!-- App pods row -->
  <text x="60" y="455" fill="#64748B" font-size="9" font-weight="600" letter-spacing="1">APPLICATION WORKLOADS (arda-app namespace)</text>

  <rect x="60" y="465" width="960" height="40" rx="6" fill="#1E293B" stroke="#475569" stroke-width="1"/>
  <rect x="65" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#6366F1" stroke-width="0.5"/>
  <text x="96" y="489" text-anchor="middle" fill="#A5B4FC" font-size="7">auth-gateway</text>
  <rect x="133" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#06B6D4" stroke-width="0.5"/>
  <text x="164" y="489" text-anchor="middle" fill="#67E8F9" font-size="7">iam-svc</text>
  <rect x="201" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#10B981" stroke-width="0.5"/>
  <text x="232" y="489" text-anchor="middle" fill="#6EE7B7" font-size="7">platform-svc</text>
  <rect x="269" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#F59E0B" stroke-width="0.5"/>
  <text x="300" y="489" text-anchor="middle" fill="#FDE68A" font-size="7">finance-svc</text>
  <rect x="337" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#8B5CF6" stroke-width="0.5"/>
  <text x="368" y="489" text-anchor="middle" fill="#C4B5FD" font-size="7">workflow-svc</text>
  <rect x="405" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#EC4899" stroke-width="0.5"/>
  <text x="436" y="489" text-anchor="middle" fill="#F9A8D4" font-size="7">crm-svc</text>
  <rect x="473" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#F97316" stroke-width="0.5"/>
  <text x="504" y="489" text-anchor="middle" fill="#FDBA74" font-size="7">hrm-svc</text>
  <rect x="541" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#14B8A6" stroke-width="0.5"/>
  <text x="572" y="489" text-anchor="middle" fill="#5EEAD4" font-size="7">notif-svc</text>
  <rect x="609" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#F97316" stroke-width="0.5"/>
  <text x="640" y="489" text-anchor="middle" fill="#FDBA74" font-size="7">media-svc</text>
  <rect x="677" y="470" width="62" height="30" rx="4" fill="#0F172A" stroke="#475569" stroke-width="0.5" stroke-dasharray="2,2"/>
  <text x="708" y="489" text-anchor="middle" fill="#64748B" font-size="7" font-style="italic">mdm-svc</text>

  <!-- Key infra -->
  <rect x="60" y="515" width="960" height="35" rx="6" fill="#1E293B" stroke="#475569" stroke-width="1"/>
  <text x="76" y="534" fill="#94A3B8" font-size="8">Platform: NATS (3-node) · Valkey (3-node) · Garage (3-node) · Zeebe 8.5 · cloudflared</text>
  <text x="76" y="546" fill="#94A3B8" font-size="8">Auth: Ory Hydra · Ory Kratos</text>

  <!-- External -->
  <rect x="60" y="560" width="140" height="20" rx="4" fill="#0F172A" stroke="#06B6D4" stroke-width="0.5"/>
  <text x="130" y="574" text-anchor="middle" fill="#22D3EE" font-size="8">🌤 Cloudflare Tunnel</text>

  <rect x="860" y="560" width="155" height="20" rx="4" fill="#0F172A" stroke="#06B6D4" stroke-width="0.5"/>
  <text x="937" y="574" text-anchor="middle" fill="#22D3EE" font-size="8">🌐 arda.io.vn</text>
</svg>
```

---

## Active Repositories

| Repository | Purpose |
| --- | --- |
| [`arda-be`](https://github.com/arda-labs/arda-be) | Go 1.26 microservices, shared libraries, protobuf definitions, NATS events, Zeebe workers |
| [`arda-mfe`](https://github.com/arda-labs/arda-mfe) | React 19 MFE shell + 7 remotes via Module Federation (Vite 8, Bun) |
| [`arda-infra`](https://github.com/arda-labs/arda-infra) | K3s manifests, Argo CD applications, Traefik config, Ory auth, CloudNativePG |
| [`.github`](https://github.com/arda-labs/.github) | Organization profile and GitHub metadata |

---

## Platform Map

### Frontend Modules

| Module | Type | Port | Stack | Description |
| --- | --- | --- | --- | --- |
| `shell` | MFE host | 5000 | React 19, Vite 8, Module Federation | Layout, auth bootstrap, navigation, lazy remote loading |
| `mfe-iam` | Remote | 5101 | React 19, shadcn/ui, Zustand | Identity & access admin — users, groups, roles, permissions |
| `mfe-platform` | Remote | 5102 | React 19, shadcn/ui, Zustand | Master data & platform admin — organizations, lookups |
| `mfe-finance` | Remote | 5103 | React 19, shadcn/ui, Zustand | Finance operations — accounts, transactions, approvals |
| `mfe-account` | Remote | 5104 | React 19, shadcn/ui, Zustand | Profile & account settings — security, sessions, devices |
| `mfe-hrm` | Remote | 5105 | React 19, shadcn/ui, Zustand | HRM admin — positions, employees, org units |
| `mfe-workflow` | Remote | 5106 | React 19, shadcn/ui, Zustand | BPMN workflow admin — case types, process config, modeler |
| `mfe-crm` | Remote | 5107 | React 19, shadcn/ui, Zustand | CRM & workbench — customers, transaction ops |

### Backend Services

| Service | Language | HTTP Port | gRPC Port | Database | Description |
| --- | --- | --- | --- | --- | --- |
| `auth-gateway` | Go | 8082 | — | — | API gateway, OAuth/OIDC proxy, forward-auth, BFF session |
| `iam-service` | Go | 8081 | — | `iam` | Identity, RBAC (Casbin), MFA, audit, login orchestration |
| `platform-service` | Go | 8091 | 9091 | `common` | Reference data, lookups, organizations, geography |
| `finance-service` | Go | 8090 | — | `finance` | Accounts, transactions, approvals, operation queues |
| `workflow-service` | Go | 8093 | 9093 | `workflow` | Workflow engine facade (Zeebe 8.5), cases, BPMN |
| `crm-service` | Go | 8094 | 9094 | `crm` | Customer relationship management, amendments |
| `hrm-service` | Go | 8097 | — | `hrm` | Positions, job titles, employees, registrations |
| `notification-service` | Go | 8095 | — | `notification` | Notifications, Web Push (FCM/APNs), NATS outbox worker |
| `media-service` | Go | 8092 | 9092 | `media` | Media storage (Garage S3) |
| `mdm-service` | Go | 8096 | — | *(scaffold)* | Master Data Management *(placeholder)* |

---

## Tech Stack

| Layer | Technology |
| --- | --- |
| **Frontend** | React 19, TypeScript 6, Vite 8, Module Federation, Tailwind CSS 4, shadcn/ui, TanStack Query, Zustand, React Hook Form + Zod, i18next + ICU |
| **Backend** | Go 1.26, `net/http` (stdlib router), gRPC, protobuf, PostgreSQL 18, pressly/goose, Casbin, NATS JetStream |
| **Identity & Auth** | Ory Hydra (OAuth2/OIDC) + Ory Kratos (identity/password), auth-gateway (BFF) |
| **Storage** | CloudNativePG (PostgreSQL 18, 3-node HA), Valkey (Redis fork, 3-node), Garage (S3-compatible, 3-node) |
| **Gateway & Ingress** | Traefik with forward-auth middleware, auth-gateway |
| **GitOps** | Argo CD, Kustomize, Image Updater |
| **Runtime** | K3s cluster (3 nodes, HA with embedded etcd), Cloudflare Tunnel, GHCR container registry |
| **Workflow** | Zeebe 8.5 (Camunda), BPMN 2.0, job workers |
| **Events** | NATS JetStream, transactional outbox pattern, `ardaevents.Envelope` |

---

## Communication Patterns

### API Routing

```
Internet → Cloudflare → arda.io.vn
  /api/*   → Traefik → auth-gateway (forward-auth) → domain services
  /assets/*, /mfes/*  → web (MFE shell static assets)
  catch-all → web (MFE shell SPA)
```

### Auth Gateway Route Map

| Route Prefix | Internal Target | Auth Required |
| --- | --- | --- |
| `/api/auth/*` | auth-gateway (self) | Public |
| `/api/kratos/*` | auth-gateway → Kratos | Public |
| `/api/iam/*`, `/api/admin/*` | iam-service | Protected |
| `/api/platform/*` | platform-service | Protected |
| `/api/finance/*` | finance-service | Protected |
| `/api/media/*` | media-service | Protected |
| `/api/workflow/*` | workflow-service | Protected |
| `/api/crm/*` | crm-service | Protected |
| `/api/notifications/*` | notification-service | Protected |

### Inter-Service Communication

| Pattern | Protocol | Use Case |
| --- | --- | --- |
| **Request/Response** | HTTP/JSON | Browser → auth-gateway → domain services |
| **Service-to-Service** | gRPC (protobuf) | Internal typed contracts, deadlines, metadata (target state) |
| **Async Events** | NATS JetStream | Domain events, notifications, cache invalidation, outbox pattern |
| **Workflow** | gRPC + Zeebe | Domain services → workflow-service → Zeebe → workers → gRPC |

---

## Workflow / BPMN Integration

```ascii
┌─────────────┐     gRPC      ┌──────────────────┐     Zeebe     ┌─────────────┐
│ Domain      │──────────────▶│  workflow-service │─────────────▶│  Zeebe 8.5  │
│ Service     │ CreateCase    │  (facade)         │               │  (engine)   │
│             │◀──────────────│                   │◀─────────────│             │
│ or MFE UI   │ SubmitCase    │  Job Workers      │  gRPC call    │             │
└─────────────┘               └──────────────────┘               └─────────────┘
                                      │
                                      │ gRPC
                                      ▼
                              ┌──────────────────┐
                              │  Domain Service  │
                              │  (business logic) │
                              └──────────────────┘
```

- **Only** `workflow-service` communicates with Zeebe
- Domain services call `workflow-service` via gRPC (`CreateCase` / `SubmitCase`)
- Job workers inside `workflow-service` call domain services via gRPC
- UI built in-house (no Camunda Tasklist/Operate/Optimize)

---

## Event System (NATS)

### Event Envelope Structure

```json
{
  "id": "uuid",
  "event_code": "notification.inbox.created",
  "schema_version": 1,
  "occurred_at": "2026-07-04T12:00:00Z",
  "source_service": "notification-service",
  "tenant_id": "uuid",
  "actor": { "user_id": "uuid" },
  "payload": { }
}
```

### Subject Naming Convention

- Subject: `arda.<domain>.<aggregate>.<action>.v1`
- Event code inside envelope: `<domain>.<aggregate>.<action>`

### Published Events (candidates)

| Event Code | Description |
| --- | --- |
| `iam.user.created` | New user registered |
| `iam.permission.changed` | User permissions updated |
| `platform.lookup.changed` | Reference data modified |
| `finance.transaction.posted` | Transaction recorded |
| `finance.approval.requested` | Approval needed |
| `workflow.task.created` | BPMN task created |
| `audit.event.recorded` | Audit trail entry |

---

## Development Environment

### Local Dev Topology

```
Developer machine
  FE dev server (localhost:5000)
  optional local BE services
    | LAN / NodePort / port-forward
    ▼
k3s cluster
  PostgreSQL (NodePort 30432)
  Valkey (NodePort 30379)
  NATS (port-forward 4222)
  Hydra admin (NodePort 30445)
  Kratos admin (NodePort 30446)
```

### Docker Compose (local backend services)

| Service | Container Port | Host Port |
| --- | --- | --- |
| iam-service | 8080 | 8081 |
| auth-gateway | 8080 | 8082 |
| mock-token | 8080 | 8083 |
| workflow-service | 8080 | 8093 |
| crm-service | 8080 | 8094 |
| notification-service | 8080 | 8095 |
| hrm-service | 8080 | 8097 |
| media-service | 8080 | 8092 |
| platform-service | 8080 (gRPC 9090) | 8091 (gRPC 9091) |

---

## Brand

| Attribute | Value |
| --- | --- |
| **Name** | ARDA Labs |
| **Fonts** | Space Grotesk for logo, Inter for text |
| **Colors** | Cyan `#06B6D4`, Indigo `#6366F1`, Midnight `#0F172A` |
| **Style** | Minimal, data-oriented, operational |
| **Slogan** | *Where data flows with intelligence.* |

---

## Links

- Website: [arda.io.vn](https://arda.io.vn)
- Contact: contact@arda.io.vn
