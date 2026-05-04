# Managed Addons

{{ product_name }} ships with fully managed addons organized around the same three pillars as the platform itself: Dev Ready, Ops Ready, and Compliance Ready.

All addons are installed, configured, upgraded, and operated by Stakater. For a full breakdown of responsibilities, see [Responsibilities](../about/responsibilities.md).

---

## Dev Ready

| Addon | What It Does |
|-------|-------------|
| [ArgoCD](./argocd/index.md) | GitOps continuous delivery engine. All deployments are driven from Git — changes committed to your repository are applied to the cluster automatically. |
| [Tronador](https://docs.stakater.com/tronador/) | Ephemeral preview environments per pull request — created automatically on PR open, torn down on merge. |
| Harbor | Private container image and Helm chart registry. Push your images and charts here; ArgoCD deploys from here. |
| [Renovate](./renovate/index.md) | Automatically opens pull requests to update application dependencies. Keeps applications current without manual effort. |
| [Forecastle](./forecastle/index.md) | A dashboard that lists and links to all applications running in your cluster — a single place to discover everything. |
| [Tilt](./tilt/index.md) | Fast local development loop for Kubernetes. Rebuilds and redeploys your application on every code change. |
| [mirrord](./mirrord/index.md) | Mirrors live cluster traffic to your local process for debugging against real requests without deploying a debug build. |
| [Reloader](./reloader/index.md) | Automatically restarts pods when their ConfigMap or Secret changes. No manual rollouts needed. |
| [Stakater Application Helm Chart](./helm-leader-chart/index.md) | A standardized Helm chart for deploying any application consistently across all environments. |

---

## Ops Ready

### Multi-Tenancy

| Addon | What It Does |
|-------|-------------|
| [Stakater MTO](./mto/index.md) | Manages namespaces, resource quotas, RBAC, and network policies across all teams. Each team gets an isolated, governed environment without cluster-admin access. |

### Observability

| Addon | What It Does |
|-------|-------------|
| [Grafana](./monitoring-stack/index.md) | Unified dashboards and visualization for all observability signals — metrics, logs, and traces in one place. |
| [Mimir](./monitoring-stack/index.md) | Scalable, long-term metrics storage and querying. Receives metrics from across all workloads. |
| [Loki](./logging-stack/index.md) | Log aggregation and querying. Application logs written to stdout are captured and indexed automatically. |
| [Tempo](./tracing/index.md) | Distributed tracing. Correlate requests across services to diagnose latency and errors. |
| [OpenTelemetry](./opentelemetry/index.md) | Telemetry collection and forwarding. Instruments your applications for metrics, logs, and traces. |
| [Alertmanager](./monitoring-stack/index.md) | Routes and deduplicates alerts. Sends notifications to PagerDuty, Slack, email, and other targets. |
| [IngressMonitorController](https://github.com/stakater/IngressMonitorController) | Automatically registers external uptime monitors for your application ingresses. Alerts when an endpoint goes down. |

### Cluster Operations

| Addon | What It Does |
|-------|-------------|
| [Velero](./velero/index.md) | Application and persistent volume backup and restore. A default backup location is provided; additional targets are supported. |
| [Descheduler](./descheduler/index.md) | Continuously rebalances pod placement across nodes to improve resource utilization and avoid hot spots. |
| [Vertical Pod Autoscaler](./vertical-pod-autoscaler/index.md) | Automatically right-sizes container resource requests based on actual usage. |
| [Horizontal Pod Autoscaler](./horizontal-pod-autoscaler/index.md) | Scales the number of pod replicas up or down based on metrics. |
| [Custom Metrics Autoscaler](./custom-metrics-autoscaler/index.md) | Scales workloads based on custom and external metrics beyond CPU and memory. |

### Networking

| Addon | What It Does |
|-------|-------------|
| [Cert-Manager](./cert-manager/index.md) | Automates TLS certificate issuance and renewal. Certificates are provisioned and rotated without manual intervention. |
| [ExternalDNS](./external-dns/index.md) | Automatically creates and updates DNS records as you create or modify services and ingresses. |
| [Istio](./service-mesh/index.md) | Service mesh providing mutual TLS between services, fine-grained traffic management, and inter-service observability. |

---

## Compliance Ready

| Addon | What It Does |
|-------|-------------|
| [OpenBao](./vault/index.md) | Open-source secrets management. Stores and manages secrets for all applications on the platform. |
| [External Secrets Operator](./external-secrets-operator/index.md) | Syncs secrets from OpenBao and supported cloud secret stores (AWS Secrets Manager, Azure Key Vault, GCP Secret Manager) into Kubernetes Secrets automatically. |
| Kyverno | Kubernetes-native policy engine. Enforces security and compliance guardrails across all tenants and workloads — preventing misconfiguration before it reaches the cluster. |
| [Keycloak](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.6) | Each {{ product_name }} account gets a dedicated Keycloak realm. Connect any identity provider your organization already uses — LDAP, SAML, OpenID Connect, or social login. |

---

## Optional Add-ons

The following components are available but not included in the base subscription.

| Addon | What It Does |
|-------|-------------|
| [RHACS](./rhacs/index.md) | Red Hat Advanced Cluster Security. Runtime threat detection, vulnerability scanning, image policy enforcement, and compliance reporting. |
| Additional Istio control planes | Multiple Istio control planes for advanced service mesh isolation between tenants or environments. Available on request. |
