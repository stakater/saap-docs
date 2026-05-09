# Service Definition

{{ product_name }} is a fully managed platform layer installed on top of a Stakater Cloud cluster. This page defines what {{ product_name }} includes and what is available as an optional add-on.

{{ product_name }} does not manage the underlying OpenShift cluster — that is Stakater Cloud's responsibility. See [Responsibilities](responsibilities.md) for the full breakdown.

---

## Dev Ready

Everything developers need to build and ship applications — without platform team involvement.

### GitOps and Deployment

| Component | What It Does |
|-----------|-------------|
| **ArgoCD** | GitOps continuous delivery engine. Git is the source of truth for all deployments — changes committed to Git are applied to the cluster automatically. |
| **GitOps repository structure** | A pre-defined, standardized layout for infrastructure and application GitOps repositories. No need to design your own structure. |
| **[Leader Helm chart](https://github.com/stakater-charts/application)** | Stakater's application Helm chart. A single, consistent way to package and deploy any application across all environments. |

### Developer Experience

| Component | What It Does |
|-----------|-------------|
| **Tronador** | Creates an ephemeral environment for every pull request — deployed automatically, torn down on merge. Developers see their changes running in a real environment before they ship. |
| **Renovate** | Automatically opens pull requests to update application dependencies. Keeps applications secure and current without manual effort. |
| **Forecastle** | A dashboard that lists and links to all applications running in your cluster — a single place to navigate everything. |
| **Tilt** | Fast local development loop for Kubernetes. Rebuilds and redeploys your application to the cluster on every code change. |
| **Reloader** | Automatically restarts pods when their ConfigMap or Secret changes. No manual rollouts needed. |

### Image and Chart Registry

| Component | What It Does |
|-----------|-------------|
| **Harbor** | A private container image and Helm chart registry. Push your images and charts here; ArgoCD deploys from here. Scoped to your cluster and tenants. |

---

## Ops Ready

Platform operations managed by {{ product_name }} and Stakater SRE — so your team does not need to.

### Multi-Tenancy

| Component | What It Does |
|-----------|-------------|
| **Stakater MTO (Multi-Tenant Operator)** | Manages namespaces, resource quotas, RBAC, and network policies across all teams on a shared cluster. Each team gets an isolated, governed environment without needing cluster-admin access. |

### Observability

{{ product_name }} includes the full LGTM stack for a unified observability experience across metrics, logs, and traces.

| Component | What It Does |
|-----------|-------------|
| **Grafana** | Unified dashboards and visualization for all observability signals — metrics, logs, and traces in one place. |
| **Mimir** | Scalable, long-term metrics storage and querying. Receives metrics from across all workloads and clusters. |
| **Loki** | Log aggregation and querying. Application logs written to stdout are captured and indexed automatically. |
| **Tempo** | Distributed tracing. Correlate requests across services to diagnose latency and errors. |
| **IngressMonitorController (IMC)** | Automatically registers external uptime monitors for your application ingresses. Alerts you when an endpoint goes down. |

### Cluster Operations

| Component | What It Does |
|-----------|-------------|
| **Autoscaling** | Horizontal Pod Autoscaler (HPA) and Vertical Pod Autoscaler (VPA) keep your workloads right-sized automatically. |
| **Velero (OADP)** | Application and persistent volume backup and restore. A default backup location is provided; additional backup targets are supported. |
| **Descheduler** | Continuously rebalances pod placement across nodes to improve resource utilization and avoid hot spots. |

### Networking

| Component | What It Does |
|-----------|-------------|
| **Cert-Manager** | Automates TLS certificate issuance and renewal. Certificates are provisioned and rotated without manual intervention. |
| **ExternalDNS** | Automatically creates and updates DNS records as you create or modify services and ingresses. |
| **Custom domains** | Bring your own domain. Point a CNAME at the cluster router hostname and configure it on your route. |

### Service Mesh

| Component | What It Does |
|-----------|-------------|
| **Istio** | Service mesh providing mutual TLS between services, fine-grained traffic management, and inter-service observability. A single control plane is provided by default; multiple control planes are available on request. |

---

## Compliance Ready

Security and governance controls built in from day one — not added later.

### Secrets Management

| Component | What It Does |
|-----------|-------------|
| **OpenBao** | Open-source secrets management (community fork of HashiCorp Vault). Stores and manages secrets for applications running on {{ product_name }}. |
| **External Secrets Operator (ESO)** | Syncs secrets from OpenBao and supported cloud secret stores (AWS Secrets Manager, Azure Key Vault, GCP Secret Manager) into Kubernetes-native Secrets automatically. |

### Policy and Access

| Component | What It Does |
|-----------|-------------|
| **Kyverno** | Kubernetes-native policy engine. Enforces security and compliance guardrails across all tenants and workloads — preventing misconfiguration before it reaches the cluster. |
| **Keycloak** | Each Stakater Cloud account gets a dedicated Keycloak realm. Connect any identity provider your organization already uses — Keycloak handles the integration. |
| **RBAC** | Role-based access control with cluster-admin, customer admin, and tenant-scoped roles. Managed through GitOps. |

### Audit and Compliance

| Component | What It Does |
|-----------|-------------|
| **Audit logging** | Cluster-level audit logs retained and accessible to authorized support staff for forensic review and incident investigation. |
| **Regulatory alignment** | Built-in controls aligned to ISO 27001, NIS2, and DORA. Declarative, GitOps-managed changes provide a full audit trail by default. |

---

## Optional Add-ons

The following components are available but not included in the base subscription.

| Add-on | Description |
|--------|-------------|
| **RHACS** | Red Hat Advanced Cluster Security. Runtime threat detection, vulnerability scanning, image policy enforcement, and compliance reporting. |
| **Additional Istio control planes** | Multiple Istio control planes for advanced service mesh isolation between tenants or environments. Available on request. |

---

## Cluster Foundation

{{ product_name }} requires a running Stakater Cloud cluster. Stakater Cloud provides and manages the underlying OpenShift infrastructure — nodes, networking, storage, upgrades, and SRE coverage. {{ product_name }} is installed on top of that cluster and does not duplicate or replace any of those responsibilities.

To get started with Stakater Cloud, contact [Stakater Support](https://support.stakater.com/index.html).

---

## Support

Support is available via the [Stakater Customer Support Portal](https://support.stakater.com/). SLAs are defined in the [Service Level Agreement](../legal-documents/sla.md).
