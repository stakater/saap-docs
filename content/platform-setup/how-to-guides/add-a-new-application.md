# Add a new application

This guide explains how to add a new application for an existing tenant in the apps GitOps repository and wire it up so ArgoCD deploys it automatically.

If the apps GitOps repository is not yet configured, start with [Configure the apps GitOps repository](../tutorials/configure-apps-gitops-repo.md) first.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `TENANT_NAME` | The tenant the application belongs to |
| `APP_NAME` | The name of the new application |
| `ENV_NAME` | The target environment (e.g. `dev`, `staging`, `prod`) |
| `CLUSTER_NAME` | Your cluster folder name in the infra repository |
| `APPS_GITOPS_REPO_URL` | The URL of your apps GitOps repository |

---

## 1. Create the application folder structure

In your apps GitOps repository, create a folder for the application under the tenant folder:

```text
apps-gitops-config/
└── TENANT_NAME/
    ├── argocd-apps/
    │   └── ENV_NAME/
    └── APP_NAME/
        └── ENV_NAME/
```

The `APP_NAME/ENV_NAME/` folder will hold the Helm values or plain YAML for the application in that environment.

---

## 2. Add the Helm chart configuration

Inside `TENANT_NAME/APP_NAME/ENV_NAME/`, create a `Chart.yaml` that references the application chart from your registry:

```yaml
apiVersion: v2
dependencies:
- name: APP_NAME
  repository: 'YOUR_HARBOR_REGISTRY_URL'
  version: 1.0.0
name: APP_NAME
version: 0.0.0
```

Create a `values.yaml` in the same folder to configure the application for this environment:

```yaml
APP_NAME:
  replicaCount: 1
  image:
    repository: YOUR_HARBOR_REGISTRY_URL/TENANT_NAME/APP_NAME
    tag: latest
```

!!! note
    Replace `YOUR_HARBOR_REGISTRY_URL` with the URL from your Harbor registry. Find it via Forecastle.

---

## 3. Create the ArgoCD Application resource

Create `TENANT_NAME/argocd-apps/ENV_NAME/APP_NAME.yaml` to tell ArgoCD where to find and deploy the application:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: TENANT_NAME-ENV_NAME-APP_NAME
  namespace: rh-openshift-gitops-instance
spec:
  destination:
    namespace: TENANT_NAME-ENV_NAME
    server: 'https://kubernetes.default.svc'
  project: TENANT_NAME
  source:
    path: TENANT_NAME/APP_NAME/ENV_NAME
    repoURL: 'APPS_GITOPS_REPO_URL'
    targetRevision: HEAD
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

---

## 4. Verify

Commit and push your changes. ArgoCD will detect the new Application resource within a few minutes.

Log in to ArgoCD and open the `TENANT_NAME-ENV_NAME` application. Confirm it has synced and the application pods are running in the `TENANT_NAME-ENV_NAME` namespace.

---

With the application deployed, continue to [Add a new environment to an application](add-a-new-environment-to-application.md) when you are ready to promote it to the next stage.
