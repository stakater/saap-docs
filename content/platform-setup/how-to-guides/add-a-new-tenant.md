# Add a new tenant

This guide explains how to add a new tenant to your cluster. A tenant represents a team or project and gets its own namespaces, resource quotas, and ArgoCD project.

If the infra GitOps repository is not yet configured, start with [Configure the infra GitOps repository](../tutorials/configure-infra-gitops-repo.md) first.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `TENANT_NAME` | The name of the new tenant |
| `CLUSTER_NAME` | Your cluster folder name in the infra repository |
| `INFRA_GITOPS_REPO_URL` | The URL of your infra GitOps repository |
| `APPS_GITOPS_REPO_URL` | The URL of your apps GitOps repository |
| `YOUR_HARBOR_REGISTRY_URL` | The URL of your Harbor registry (find it via Forecastle) |

---

## 1. Create the Tenant resource

In your infra GitOps repository, create a `Tenant` resource at `CLUSTER_NAME/tenant-operator-config/tenants/TENANT_NAME.yaml`:

```yaml
apiVersion: tenantoperator.stakater.com/v1beta1
kind: Tenant
metadata:
  name: TENANT_NAME
spec:
  quota: TENANT_NAME-large
  owners:
    users:
    - your-user@example.com
  argocd:
    sourceRepos:
    - 'INFRA_GITOPS_REPO_URL'
    - 'APPS_GITOPS_REPO_URL'
    - 'YOUR_HARBOR_REGISTRY_URL'
  templateInstances:
  - spec:
      template: tenant-vault-access
      sync: true
  namespaces:
  - dev
  - staging
  - prod
```

Adjust `owners.users`, `sourceRepos`, and `namespaces` to match your team and environment setup.

---

## 2. Create the Quota resource

Create a matching `Quota` resource at `CLUSTER_NAME/tenant-operator-config/quotas/TENANT_NAME-large.yaml`. The name must match the value in `spec.quota` of the Tenant above.

```yaml
apiVersion: tenantoperator.stakater.com/v1beta1
kind: Quota
metadata:
  name: TENANT_NAME-large
  annotations:
    quota.tenantoperator.stakater.com/is-default: "false"
spec:
  resourcequota:
    hard:
      requests.cpu: "16"
      requests.memory: 32Gi
  limitrange:
    limits:
      - defaultRequest:
          cpu: 10m
          memory: 50Mi
        type: Container
```

Adjust the `requests.cpu` and `requests.memory` limits to fit your team's expected workload.

---

## 3. Verify

Commit and push your changes. ArgoCD will apply the new `Tenant` and `Quota` resources within a few minutes.

Log in to ArgoCD and open the `CLUSTER_NAME-tenant-operator-config` application. Confirm both resources have synced successfully and the new tenant namespaces are visible in the cluster.

---

With the tenant created, continue to [Add a new application](add-a-new-application.md) to deploy workloads into it.
