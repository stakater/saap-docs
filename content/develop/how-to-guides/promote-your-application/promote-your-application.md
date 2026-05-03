# Promote your application

This guide explains how to promote an application from one environment to the next by updating the chart version and image tag in your apps GitOps repository.

Promotion means copying the verified versions from a source environment into the target environment's configuration. ArgoCD detects the change and deploys automatically.

This guide assumes your application is already deployed in at least one environment. If not, start with [Deploy with ArgoCD and Helm](../deploy-app-with-argocd-and-helm/deploy-app-with-argocd-and-helm.md) first.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `TENANT_NAME` | Your tenant name |
| `APP_NAME` | Your application name |
| `SOURCE_ENV` | The environment you are promoting from (e.g. `dev`) |
| `TARGET_ENV` | The environment you are promoting to (e.g. `staging`) |
| `APPS_GITOPS_REPO_URL` | The URL of your apps GitOps repository |

---

## 1. Promote the chart version

Open `TENANT_NAME/APP_NAME/SOURCE_ENV/Chart.yaml` in your apps GitOps repository and note the chart version:

```yaml
apiVersion: v2
dependencies:
  - name: APP_NAME
    repository: HARBOR_HELM_REPO_URL
    version: 1.0.51
name: APP_NAME
version: 1.0.51
```

Copy that version into `TENANT_NAME/APP_NAME/TARGET_ENV/Chart.yaml`.

---

## 2. Promote the image tag

Open `TENANT_NAME/APP_NAME/SOURCE_ENV/values.yaml` and note the image tag:

```yaml
APP_NAME:
  application:
    deployment:
      image:
        repository: HARBOR_REGISTRY_URL/TENANT_NAME/APP_NAME
        tag: 1.0.51
```

Copy that tag into `TENANT_NAME/APP_NAME/TARGET_ENV/values.yaml`.

---

## 3. Commit and verify

Commit and push your changes. ArgoCD detects the update and redeploys the application in `TARGET_ENV` within a few minutes.

Log in to ArgoCD and confirm the `TENANT_NAME-TARGET_ENV-APP_NAME` application has synced and the pods are running.

---

To add an entirely new environment to an application, see [Add a new environment](../../../platform-setup/how-to-guides/add-a-new-environment-to-application.md).
