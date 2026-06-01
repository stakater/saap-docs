# Responsibilities

{{ product_name }} follows a clear shared responsibility model. Stakater manages the platform — you manage your applications.

## What Stakater Manages

Stakater is fully responsible for the health, availability, and operation of both the underlying Stakater Cloud cluster and the {{ product_name }} platform layer installed on top of it.

### Stakater Cloud (cluster infrastructure)

- Provisioning, scaling, and decommissioning of cluster nodes
- Control plane and infrastructure node management
- Cluster upgrades and security patching
- Cluster networking, storage, and load balancer infrastructure
- Cluster-level monitoring, alerting, and incident response
- SLA coverage and SRE on-call

### {{ product_name }} (platform layer)

- Installation, configuration, and upgrades of all platform components (ArgoCD, MTO, Harbor, OpenBao, Kyverno, LGTM stack, Istio, Cert-Manager, and all other included components)
- Availability and health monitoring of platform components
- Security patching for all platform components
- Stakater Identity realm provisioning for each customer account

## What You Manage

You are responsible for everything that runs on top of the platform — your applications, configurations, and data.

### Applications and workloads

- Full lifecycle of your applications: deployment, configuration, versioning, resource limits, and scaling
- Application health monitoring and alerting
- Application-level incident response and on-call
- Container images and Helm charts pushed to Harbor

### GitOps configuration

- Your infra and app GitOps repository content
- ArgoCD Application and ApplicationSet definitions
- Tenant and namespace configuration via MTO
- Kyverno policy customizations within your tenant scope

### Secrets and data

- Secrets stored in OpenBao and their rotation schedules
- Application data and databases
- Application backup schedules and restore procedures (using Velero)

### Identity and access

- Connecting your identity provider to your Stakater Identity realm
- Managing users, groups, and roles within your realm
- RBAC assignments within your tenants

## Change Management

All changes to the platform layer are owned and executed by Stakater. Cluster upgrades are scheduled with advance notice and can be coordinated via the [Stakater Customer Support Portal](https://support.stakater.com/).

Changes to your applications and GitOps configurations are owned entirely by you. Because {{ product_name }} uses a GitOps model, all changes to your workloads are version-controlled and auditable by default.
