# Managed Addons

{{ product_name }} ships with fully managed addons grouped by the same four areas as the top-level nav: Deploy, Develop, Observe, and Govern. The Govern category covers active security and the audit-ready compliance posture (multi-tenancy, secrets, policy, backup, vulnerability scanning).

All addons are installed, configured, upgraded, and operated by Stakater. For a full breakdown of responsibilities, see [Responsibilities](../about/responsibilities.md).

---

## Deploy

GitOps delivery, production networking, and runtime sizing — the components that get your code into production and keep it healthy there.

| Addon | What It Does |
|-------|-------------|
| [ArgoCD](./argocd/index.md) | GitOps continuous delivery engine. All deployments are driven from Git — changes committed to your repository are applied to the cluster automatically. |
| [Tronador](https://docs.stakater.com/tronador/) | Ephemeral preview environments per pull request — created automatically on PR open, torn down on merge. |
| [Cert-Manager](./cert-manager/index.md) | Automates TLS certificate issuance and renewal. Certificates are provisioned and rotated without manual intervention. |
| [ExternalDNS](./external-dns/index.md) | Automatically creates and updates DNS records as you create or modify services and ingresses. |
| [Istio](./service-mesh/index.md) | Service mesh providing mutual TLS between services, fine-grained traffic management, and inter-service observability. |
| [Vertical Pod Autoscaler](./vertical-pod-autoscaler/index.md) | Automatically right-sizes container resource requests based on actual usage. |
| [Horizontal Pod Autoscaler](./horizontal-pod-autoscaler/index.md) | Scales the number of pod replicas up or down based on metrics. |
| [Custom Metrics Autoscaler](./custom-metrics-autoscaler/index.md) | Scales workloads based on custom and external metrics beyond CPU and memory. |
| [Descheduler](./descheduler/index.md) | Continuously rebalances pod placement across nodes to improve resource utilization and avoid hot spots. |

---

## Develop

Local iteration, dependency management, and the building blocks for your application code.

| Addon | What It Does |
|-------|-------------|
| Harbor | Private container image and Helm chart registry. Push your images and charts here; ArgoCD deploys from here. |
| [Renovate](./renovate/index.md) | Automatically opens pull requests to update application dependencies. Keeps applications current without manual effort. |
| [Forecastle](./forecastle/index.md) | A dashboard that lists and links to all applications running in your cluster — a single place to discover everything. |
| [Tilt](./tilt/index.md) | Fast local development loop for Kubernetes. Rebuilds and redeploys your application on every code change. |
| [mirrord](./mirrord/index.md) | Mirrors live cluster traffic to your local process for debugging against real requests without deploying a debug build. |
| [Reloader](./reloader/index.md) | Automatically restarts pods when their ConfigMap or Secret changes. No manual rollouts needed. |
| [Stakater Application Helm Chart](./helm-leader-chart/index.md) | A standardized Helm chart for deploying any application consistently across all environments. |
| PostgreSQL | Managed relational database for your applications. |
| Redis | Managed in-memory data store and cache for your applications. |

---

## Observe

| Addon | What It Does |
|-------|-------------|
| [Grafana](./grafana/index.md) | Unified dashboards and visualization for all observability signals — metrics, logs, and traces in one place. |
| [Mimir](./mimir/index.md) | Scalable, long-term metrics storage and querying. Receives metrics emitted over OTLP from your workloads. |
| [Loki](./loki/index.md) | Log aggregation and querying. Application logs emitted over OTLP are indexed automatically. |
| [Tempo](./tempo/index.md) | Distributed tracing. Correlate requests across services to diagnose latency and errors. |
| [OpenTelemetry](./opentelemetry/index.md) | Telemetry collection and forwarding. The single ingestion endpoint for metrics, logs, and traces. |
| [Alertmanager](./alertmanager/index.md) | Routes and deduplicates alerts. Sends notifications to PagerDuty, Slack, email, and other targets. |
| [IngressMonitorController](./imc/index.md) | Automatically registers external uptime monitors for your application ingresses. Alerts when an endpoint goes down. |

---

## Govern

Multi-tenancy, secrets management, policy enforcement, backup, and vulnerability scanning — the governance and compliance posture you carry into audits.

| Addon | What It Does |
|-------|-------------|
| [Stakater MTO](./mto/index.md) | Manages namespaces, resource quotas, RBAC, and network policies across all teams. Each team gets an isolated, governed environment without cluster-admin access. |
| [Velero](./velero/index.md) | Application and persistent volume backup and restore. A default backup location is provided; additional targets are supported. |
| [Kyverno](./kyverno/index.md) | Kubernetes-native policy engine. Enforces security and compliance guardrails across all tenants and workloads — preventing misconfiguration before it reaches the cluster. |
| [OpenBao](./vault/index.md) | Open-source secrets management. Stores and manages secrets for all applications on the platform. |
| [External Secrets Operator](./external-secrets-operator/index.md) | Syncs secrets from OpenBao and supported cloud secret stores (AWS Secrets Manager, Azure Key Vault, GCP Secret Manager) into Kubernetes Secrets automatically. |
| [RHACS](./rhacs/index.md) *(optional)* | Red Hat Advanced Cluster Security. Runtime threat detection, vulnerability scanning, image policy enforcement, and compliance reporting. Available on request — not included in the base subscription. |

---

## Optional Add-ons

The following components are available but not included in the base subscription.

| Addon | What It Does |
|-------|-------------|
| Additional Istio control planes | Multiple Istio control planes for advanced service mesh isolation between tenants or environments. Available on request. |
