# Service Definition

{{ product_name }} is a fully managed platform layer installed on top of a Stakater Cloud cluster. This page defines what {{ product_name }} includes and what is available as an optional add-on.

{{ product_name }} does not manage the underlying OpenShift cluster — that is Stakater Cloud's responsibility. See [Responsibilities](responsibilities.md) for the full breakdown.

---

## Deploy

GitOps delivery, production networking, and runtime sizing — what gets your code into production and keeps it healthy there.

### GitOps and Delivery

| Component | What It Does |
|-----------|-------------|
| **ArgoCD** | GitOps continuous delivery engine. Git is the source of truth for all deployments — changes committed to Git are applied to the cluster automatically. |
| **GitOps repository structure** | A pre-defined, standardized layout for infrastructure and application GitOps repositories. No need to design your own structure. |
| **Tronador** | Creates an ephemeral environment for every pull request — deployed automatically, torn down on merge. Developers see their changes running in a real environment before they ship. |

### Networking

| Component | What It Does |
|-----------|-------------|
| **Cert-Manager** | Automates TLS certificate issuance and renewal. Certificates are provisioned and rotated without manual intervention. |
| **ExternalDNS** | Automatically creates and updates DNS records as you create or modify services and ingresses. |
| **Custom domains** | Bring your own domain. Point a CNAME at the cluster router hostname and configure it on your route. |
| **Istio** | Service mesh providing mutual TLS between services, fine-grained traffic management, and inter-service observability. A single control plane is provided by default; multiple control planes are available on request. |

### Runtime Sizing

| Component | What It Does |
|-----------|-------------|
| **Autoscaling** | Horizontal Pod Autoscaler (HPA), Vertical Pod Autoscaler (VPA), and Custom Metrics Autoscaler keep your workloads right-sized automatically. |
| **Descheduler** | Continuously rebalances pod placement across nodes to improve resource utilization and avoid hot spots. |

---

## Develop

Local iteration, dependency management, and the building blocks for your application code.

### Developer Experience

| Component | What It Does |
|-----------|-------------|
| **[Leader Helm chart](https://github.com/stakater-charts/application)** | Stakater's application Helm chart. A single, consistent way to package and deploy any application across all environments. |
| **Tilt** | Fast local development loop for Kubernetes. Rebuilds and redeploys your application to the cluster on every code change. |
| **mirrord** | Mirrors live cluster traffic to your local process for debugging against real requests without deploying a debug build. |
| **Reloader** | Automatically restarts pods when their ConfigMap or Secret changes. No manual rollouts needed. |
| **Renovate** | Automatically opens pull requests to update application dependencies. Keeps applications secure and current without manual effort. |
| **Forecastle** | A dashboard that lists and links to all applications running in your cluster — a single place to navigate everything. |

### Image and Chart Registry

| Component | What It Does |
|-----------|-------------|
| **Harbor** | A private container image and Helm chart registry. Push your images and charts here; ArgoCD deploys from here. Scoped to your cluster and tenants. |

### Application Data

| Component | What It Does |
|-----------|-------------|
| **PostgreSQL** | Managed relational database for your applications. |
| **Redis** | Managed in-memory data store and cache for your applications. |

---

## Observe

{{ product_name }} includes the full LGTM stack for a unified observability experience across metrics, logs, and traces.

| Component | What It Does |
|-----------|-------------|
| **Grafana** | Unified dashboards and visualization for all observability signals — metrics, logs, and traces in one place. |
| **Mimir** | Scalable, long-term metrics storage and querying. Receives metrics from across all workloads and clusters. |
| **Loki** | Log aggregation and querying. Application logs written to stdout are captured and indexed automatically. |
| **Tempo** | Distributed tracing. Correlate requests across services to diagnose latency and errors. |
| **OpenTelemetry Collector** | Single OTLP ingestion endpoint for metrics, logs, and traces. |
| **Alertmanager** | Routes and deduplicates alerts. Sends notifications to PagerDuty, Slack, email, or webhooks. |
| **IngressMonitorController (IMC)** | Automatically registers external uptime monitors for your application ingresses. Alerts you when an endpoint goes down. |

---

## Govern

Multi-tenancy, secrets, policy, backup, and vulnerability scanning — the governance and compliance posture built in from day one, not added later.

### Multi-Tenancy

| Component | What It Does |
|-----------|-------------|
| **Stakater MTO (Multi-Tenant Operator)** | Manages namespaces, resource quotas, RBAC, and network policies across all teams on a shared cluster. Each team gets an isolated, governed environment without needing cluster-admin access. |

### Secrets Management

| Component | What It Does |
|-----------|-------------|
| **OpenBao** | Open-source secrets management (community fork of HashiCorp Vault). Stores and manages secrets for applications running on {{ product_name }}. |
| **External Secrets Operator (ESO)** | Syncs secrets from OpenBao and supported cloud secret stores (AWS Secrets Manager, Azure Key Vault, GCP Secret Manager) into Kubernetes-native Secrets automatically. |

### Policy and Access

| Component | What It Does |
|-----------|-------------|
| **Kyverno** | Kubernetes-native policy engine. Enforces security and compliance guardrails across all tenants and workloads — preventing misconfiguration before it reaches the cluster. |
| **[Stakater Identity](../platform-setup/explanation/stakater-identity.md)** | Each Stakater Cloud account gets a dedicated realm. Connect any identity provider your organization already uses — Stakater Identity handles the federation. |
| **RBAC** | Role-based access control with cluster-admin, customer admin, and tenant-scoped roles. Managed through GitOps. |

### Backup and Audit

| Component | What It Does |
|-----------|-------------|
| **Velero (OADP)** | Application and persistent volume backup and restore. A default backup location is provided; additional backup targets are supported. |
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
