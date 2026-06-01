# What is {{ product_name }}?

**{{ product_name }}** is a ready-to-run application delivery and developer platform — designed, built, and operated by Stakater on top of **Stakater Cloud** (managed OpenShift).

It unifies everything your engineering teams need to build, deploy, operate, and govern applications. Teams that run {{ product_name }} do not need a dedicated platform engineering team.

> **Dev Ready. Ops Ready. Compliance Ready.**

## The Problem It Solves

Organizations building on Kubernetes typically hit the same wall:

- Developers wait on platform engineers for environments, access, and pipeline setup — instead of shipping value.
- Operations teams spend their time on toil: patching clusters, managing certificates, wiring observability — instead of reliability.
- Compliance and security are handled reactively, manually, and always too late.

The result is a hidden platform team tax — one that grows with every new team you add and never goes away.

**{{ product_name }} eliminates that tax.**

## What You Get

{{ product_name }} delivers on those three promises through four areas your teams work in — Deploy, Develop, Observe, and Govern — each fully managed so your team focuses on applications, not platform.

### Deploy

GitOps continuous delivery, production networking, and runtime sizing — what gets your code into production and keeps it healthy there.

- ArgoCD as the GitOps engine — every cluster change is a Git commit, applied automatically
- Tronador for ephemeral preview environments per pull request
- Cert-Manager for automated TLS certificate issuance and renewal
- ExternalDNS for automatic DNS record management
- Istio service mesh for mutual TLS and fine-grained traffic management
- Horizontal, vertical, and custom-metrics autoscaling
- Descheduler to rebalance workloads as conditions change

### Develop

Developers get instant, secure environments and everything they need to ship — without waiting on anyone.

- Self-service tenant namespaces and environments provisioned automatically via GitOps
- [Leader Helm chart](https://github.com/stakater-charts/application) — a standardized application chart for consistent deployments across all environments
- Harbor registry for storing and distributing your container images and Helm charts
- Tilt for fast local development and testing against the cluster
- mirrord for debugging local code against live cluster traffic
- Reloader to auto-roll pods when ConfigMaps or Secrets change
- Renovate for automated dependency updates
- Forecastle dashboard for discovering and navigating all running applications
- Managed PostgreSQL and Redis for application data

### Observe

Metrics, logs, traces, alerts, dashboards, and uptime monitoring — all on the OpenTelemetry-first LGTM stack.

- Mimir for long-term metrics storage; Loki for log aggregation; Tempo for distributed tracing
- Grafana as the single visualization layer for every signal
- Alertmanager routes metric and log alerts to Slack, PagerDuty, email, or webhooks
- OpenTelemetry collector as the single OTLP ingestion endpoint for all three signals
- IngressMonitorController + UptimeRobot for external uptime probes against your public endpoints

### Govern

Multi-tenancy, secrets, policy, backup, and vulnerability scanning — the governance and compliance posture built in from day one, not added later.

- Policy-driven multi-tenancy via Stakater MTO — namespaces, quotas, and RBAC across all teams managed automatically
- OpenBao for secrets management, synced to clusters via External Secrets Operator
- Kyverno for policy enforcement across all tenants and workloads
- Velero for automated backup and restore of applications and persistent volumes
- Audit logging retained at the cluster level
- Built-in controls aligned to ISO 27001, NIS2, and DORA
- Stakater Identity with a dedicated realm per account — connect any identity provider your organization already uses

## Built on Stakater Cloud

{{ product_name }} is available exclusively on **Stakater Cloud** — Stakater's fully managed OpenShift service. Stakater SRE manages the underlying infrastructure so your teams focus entirely on applications.

See [Responsibilities](about/responsibilities.md) for a clear breakdown of what Stakater owns and what you own.

## Where to Go Next

| I want to... | Go to |
|---|---|
| See exactly what's included | [Service Definition](about/service-definition.md) |
| Understand what Stakater manages vs what you own | [Responsibilities](about/responsibilities.md) |
| Set up GitOps repositories and configure the platform | [Platform Setup](platform-setup/index.md) |
| Deploy my first application | [Deploy Your First App](develop/tutorials/deploy-demo-app.md) |
| Start the inner development loop | [Inner Loop](develop/tutorials/inner-loop/prepare-environment/prepare-env.md) |
| Review compliance and regulatory coverage | [Govern](govern/index.md) |
| Browse available platform components | [Managed Addons](managed-addons/overview.md) |
