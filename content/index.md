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

{{ product_name }} is organized around three pillars, each covering a domain your teams would otherwise need to build and maintain themselves.

### Dev Ready

Developers get instant, secure environments and everything they need to ship — without waiting on anyone.

- Self-service tenant namespaces and environments provisioned automatically via GitOps
- Pre-defined GitOps repository structure with ArgoCD managing all deployments declaratively
- [Leader Helm chart](https://github.com/stakater-charts/application) — a standardized application chart for consistent deployments across all environments
- Ephemeral preview environments per pull request via Tronador — created automatically, torn down on merge
- Harbor registry for storing and distributing your container images and Helm charts
- Renovate for automated dependency updates
- Forecastle dashboard for discovering and navigating all running applications
- Tilt for fast local development and testing against the cluster

### Ops Ready

Platform operations are handled by {{ product_name }} and Stakater SRE — not your team.

- Policy-driven multi-tenancy via Stakater MTO — namespaces, quotas, and RBAC across all teams managed automatically
- LGTM observability stack — Grafana, Loki, Tempo, and Mimir for dashboards, logs, traces, and metrics
- Application uptime monitoring via IngressMonitorController
- Automated backup and restore for applications and persistent volumes via Velero
- Istio service mesh for traffic management and inter-service security
- Horizontal and vertical pod autoscaling
- Cert-Manager for automated TLS certificate issuance and renewal
- ExternalDNS for automatic DNS record management
- Cluster lifecycle managed by Stakater SRE: upgrades, patching, and incident response

### Compliance Ready

Security and governance controls are built in from day one — not added later.

- OpenBao for secrets management, synced to clusters via External Secrets Operator
- Kyverno for policy enforcement across all tenants and workloads
- Audit logging retained at the cluster level
- Built-in controls aligned to ISO 27001, NIS2, and DORA
- Keycloak-based authentication with a dedicated realm per account — connect any identity provider your organization already uses

## Built on Stakater Cloud

{{ product_name }} is available exclusively on **Stakater Cloud** — Stakater's fully managed OpenShift service. Stakater SRE manages the underlying infrastructure so your teams focus entirely on applications.

See [Responsibilities](about/responsibilities.md) for a clear breakdown of what Stakater owns and what you own.

## Where to Go Next

| I want to... | Go to |
|---|---|
| See exactly what's included | [Service Definition](about/service-definition.md) |
| Understand what Stakater manages vs what you own | [Responsibilities](about/responsibilities.md) |
| Set up GitOps repositories and configure the platform | [Platform Setup](platform-setup/overview.md) |
| Deploy my first application | [Deploy Your First App](develop/tutorials/deploy-demo-app.md) |
| Start the inner development loop | [Inner Loop](develop/tutorials/inner-loop/prepare-environment/prepare-env.md) |
| Review compliance and regulatory coverage | [Security & Compliance](secure/overview.md) |
| Browse available platform components | [Managed Addons](managed-addons/overview.md) |
