# Deploy a new version via GitOps

By the end of this guide, a new image and chart version will be deployed to your environment — no `kubectl` or `helm` CLI required. You update the version references in the apps GitOps repository and ArgoCD applies the change automatically.

This guide assumes your application is already onboarded in the apps GitOps repository. If it is not, complete [Add a new application](../../../platform-setup/how-to-guides/add-a-new-application.md) first.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `TENANT_NAME` | Your tenant name |
| `APP_NAME` | Your application name |
| `ENV_NAME` | The target environment (e.g. `dev`) |
| `CHART_VERSION` | The new chart version in Harbor (e.g. `1.0.1`) |
| `IMAGE_TAG` | The new image tag in Harbor (e.g. `1.0.1`) |
| `HARBOR_HELM_REPO_URL` | The Helm registry URL from Harbor |
| `HARBOR_REGISTRY_URL` | The Docker registry URL from Harbor |

---

## 1. Update the chart version

In your apps GitOps repository, open `TENANT_NAME/APP_NAME/ENV_NAME/Chart.yaml` and update the dependency version to the new chart version:

```yaml
apiVersion: v2
name: APP_NAME
description: A Helm chart for Kubernetes
dependencies:
  - name: APP_NAME
    version: CHART_VERSION
    repository: HARBOR_HELM_REPO_URL
version: CHART_VERSION
```

---

## 2. Update the image tag

Open `TENANT_NAME/APP_NAME/ENV_NAME/values.yaml` and update the image tag:

```yaml
APP_NAME:
  application:
    deployment:
      image:
        repository: HARBOR_REGISTRY_URL/TENANT_NAME/APP_NAME
        tag: IMAGE_TAG
```

---

## 3. Commit and push

```bash
git add TENANT_NAME/APP_NAME/ENV_NAME/
git commit -m "chore: deploy APP_NAME CHART_VERSION to ENV_NAME"
git push
```

ArgoCD detects the commit within seconds and begins syncing the new version to the `TENANT_NAME-ENV_NAME` namespace.

---

## 4. Verify

Log in to ArgoCD via Forecastle. Open the `TENANT_NAME-ENV_NAME-APP_NAME` application and confirm it has synced successfully and the new version is running.

In the OpenShift console, navigate to **Workloads > Pods** in the `TENANT_NAME-ENV_NAME` namespace and confirm the pods are healthy.

---

With the application running in `ENV_NAME`, continue to [Promote your application](../promote-your-application/promote-your-application.md) when you are ready to release it to the next environment.
