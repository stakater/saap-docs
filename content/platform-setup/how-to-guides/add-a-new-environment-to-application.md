# Add a new environment

By the end of this guide, a new environment folder, ArgoCD Application, and root watcher will be committed to your apps GitOps repository and ArgoCD will begin deploying to it.

If the apps GitOps repository is not yet configured, start with [Configure the apps GitOps repository](../tutorials/configure-apps-gitops-repo.md) first.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `TENANT_NAME` | Your tenant name |
| `APP_NAME` | Your application name |
| `ENV_NAME` | The new environment name (e.g. `prod`) |
| `CLUSTER_NAME` | Your cluster folder name |
| `APPS_GITOPS_REPO_URL` | The URL of your apps GitOps repository |

---

## 1. Create the environment folder

In your apps GitOps repository, navigate to `TENANT_NAME/APP_NAME/` and create a folder named after the new environment:

```text
TENANT_NAME/
└── APP_NAME/
    └── ENV_NAME/
```

---

## 2. Add the Helm chart configuration

Inside the `ENV_NAME` folder, add `Chart.yaml` and `values.yaml` with configuration specific to this environment. Add a `templates/` folder for any additional Kubernetes resources:

```text
TENANT_NAME/
└── APP_NAME/
    └── ENV_NAME/
        ├── Chart.yaml
        ├── values.yaml
        └── templates/
```

---

## 3. Create a tenant-level ArgoCD Application

In the tenant's `argocd-apps` folder, create an ArgoCD Application that points to the environment folder you just created.

Add `TENANT_NAME/argocd-apps/ENV_NAME/APP_NAME.yaml`:

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

## 4. Create a root-level ArgoCD Application

At the root of the apps repository, create an ArgoCD Application that points to the tenant's `argocd-apps/ENV_NAME` folder. This tells ArgoCD to watch all tenant-level applications for this environment.

Add `argocd-apps/CLUSTER_NAME/TENANT_NAME-ENV_NAME.yaml`:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: TENANT_NAME-ENV_NAME
  namespace: rh-openshift-gitops-instance
spec:
  destination:
    namespace: rh-openshift-gitops-instance
    server: 'https://kubernetes.default.svc'
  project: TENANT_NAME
  source:
    path: TENANT_NAME/argocd-apps/ENV_NAME
    repoURL: 'APPS_GITOPS_REPO_URL'
    targetRevision: HEAD
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

---

## 5. Verify the infra repository is watching this cluster

The infra repository must have an ArgoCD Application pointing to `argocd-apps/CLUSTER_NAME/` in the apps repository. If this is an existing cluster, this application already exists. If this is a new cluster, add it now — see [Link the apps repository to the infra repository](../tutorials/configure-apps-gitops-repo.md#5-link-the-apps-repository-to-the-infra-repository).

---

Commit and push your changes. ArgoCD will pick up the new application and deploy the environment within a few minutes.
