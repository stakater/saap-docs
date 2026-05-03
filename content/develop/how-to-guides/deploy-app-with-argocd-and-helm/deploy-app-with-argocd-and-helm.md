# Deploy an application with ArgoCD and Helm

This guide walks through deploying a Helm chart from Harbor using both the Helm CLI and the ArgoCD UI, so you can verify the application is running and understand how ArgoCD manages it.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `TENANT_NAME` | Your tenant name |
| `APP_NAME` | Your application name |
| `HARBOR_HELM_REPO_NAME` | A local alias for the Harbor Helm repository |
| `HARBOR_HELM_REPO_URL` | The Helm registry URL from Harbor (find it via Forecastle) |
| `HARBOR_HELM_REGISTRY_URL` | The OCI or HTTPS URL used by ArgoCD to source the chart |
| `CHART_VERSION` | The chart version to deploy |

---

## 1. Add the Harbor Helm repository

```bash
helm repo add HARBOR_HELM_REPO_NAME HARBOR_HELM_REPO_URL
helm repo update
```

---

## 2. Install the chart

```bash
helm install APP_NAME HARBOR_HELM_REPO_NAME/APP_NAME \
  --version CHART_VERSION \
  --namespace TENANT_NAME-dev
```

Verify the pods are running:

```bash
oc get pods -n TENANT_NAME-dev
```

---

## 3. Test the application

Port-forward to your local machine and send a test request:

```bash
oc port-forward deployment/APP_NAME 8080:8080 -n TENANT_NAME-dev
curl localhost:8080
```

---

## 4. Scale using Helm

Use `helm upgrade` to change the replica count:

```bash
helm upgrade APP_NAME HARBOR_HELM_REPO_NAME/APP_NAME \
  --set APP_NAME.deployment.replicas=3 \
  --namespace TENANT_NAME-dev
```

Verify the scale-up:

```bash
oc get pods -n TENANT_NAME-dev
```

---

## 5. Clean up

Remove the Helm release when you are done:

```bash
helm uninstall APP_NAME --namespace TENANT_NAME-dev
```

---

## 6. Deploy via the ArgoCD UI

For GitOps-managed deployments, use ArgoCD instead of the Helm CLI directly.

1. Log in to the ArgoCD UI.
1. Click **+ NEW APP** and fill in the following:

    **GENERAL**
    - Application Name: `TENANT_NAME-APP_NAME`
    - Project: `TENANT_NAME`
    - Sync Policy: `Automatic`

    **SOURCE**
    - Repository URL: `HARBOR_HELM_REGISTRY_URL`
    - Select `Helm` from the type dropdown
    - Chart: `APP_NAME`
    - Version: `CHART_VERSION`

    **DESTINATION**
    - Cluster URL: `https://kubernetes.default.svc`
    - Namespace: `TENANT_NAME-dev`

1. Click **Create**. ArgoCD deploys the application and displays all Kubernetes resources it manages.
1. Navigate to **Workloads > Pods** in the `TENANT_NAME-dev` namespace of the OpenShift console to confirm the pods are running.

---

With the application deployed, continue to [Promote your application](../promote-your-application/promote-your-application.md) when you are ready to release it to the next environment.
