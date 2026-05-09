# Promote your application

This tutorial walks through promoting an application from `dev` to `staging` by updating the chart version and image tag in your apps GitOps repository.

This tutorial assumes your application is already deployed in the `dev` environment via the apps GitOps repository. If not, complete [Deploy a demo app](../../deploy-demo-app.md) first.

Replace the following placeholders with your own values:

| Placeholder | Description |
|---|---|
| `TENANT_NAME` | Your tenant name |
| `APP_NAME` | Your application name |
| `SOURCE_ENV` | The environment you are promoting from (e.g. `dev`) |
| `TARGET_ENV` | The environment you are promoting to (e.g. `staging`) |

---

## 1. Check the current version in the source environment

Open `TENANT_NAME/APP_NAME/SOURCE_ENV/Chart.yaml` in your apps GitOps repository:

```yaml
apiVersion: v2
dependencies:
  - name: APP_NAME
    repository: HARBOR_HELM_REPO_URL
    version: 1.0.51
name: APP_NAME
version: 1.0.51
```

Note the version — you will copy it to the target environment.

---

## 2. Update the target environment

Open `TENANT_NAME/APP_NAME/TARGET_ENV/Chart.yaml` and set the same version:

```yaml
apiVersion: v2
dependencies:
  - name: APP_NAME
    repository: HARBOR_HELM_REPO_URL
    version: 1.0.51
name: APP_NAME
version: 1.0.51
```

Open `TENANT_NAME/APP_NAME/TARGET_ENV/values.yaml` and update the image tag to match:

```yaml
APP_NAME:
  application:
    deployment:
      image:
        repository: HARBOR_REGISTRY_URL/TENANT_NAME/APP_NAME
        tag: 1.0.51
```

---

## 3. Commit and verify

Commit and push your changes. Log in to ArgoCD and confirm the `TENANT_NAME-TARGET_ENV-APP_NAME` application has synced and the pods are running in the `TENANT_NAME-TARGET_ENV` namespace.

---

You have promoted the application through one environment. Repeat the same steps for each subsequent environment.
