# Multi-Tenant Operator

Multi-Tenant Operator manages multi-tenancy on the platform. It enforces namespace isolation, resource quotas, network policies, and RBAC for every tenant automatically — without requiring cluster-admin access.

Each team operates within their own tenant in full autonomy. Changes to tenant configuration in the infra GitOps repository are applied across all the tenant's namespaces automatically.

For full configuration reference, see the [Multi-Tenant Operator documentation](https://docs.stakater.com/mto/).
