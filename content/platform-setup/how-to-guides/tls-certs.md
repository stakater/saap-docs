# Configure TLS certificates

This guide explains how to provision a wildcard TLS certificate using cert-manager with a DNS-01 challenge, distribute it across tenant namespaces, and validate the result.

Use this approach when you need wildcard coverage (e.g. `*.example.com`) or when your cluster is not publicly reachable from the internet. If you have a single publicly reachable hostname, [http-01 challenges](http01-certs.md) require no DNS provider credentials and are simpler to set up.

**Prerequisites:**

- A `ClusterIssuer` is configured on your cluster. Confirm the name with your cluster administrator before starting.
- You have DNS provider credentials with permission to create `TXT` records (needed to complete the DNS-01 challenge).

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `CLUSTER_NAME` | Your cluster folder name in the infra repository |
| `TENANT_NAME` | The tenant that owns the certificate |
| `TENANT_SYSTEM_NAMESPACE` | The tenant's system namespace (confirm with your cluster administrator) |
| `TLS_SECRET_NAME` | The name of the Kubernetes secret cert-manager will create |
| `CLUSTER_ISSUER_NAME` | The name of the `ClusterIssuer` on your cluster |
| `INFRA_GITOPS_REPO_URL` | The URL of your infra GitOps repository |

---

## 1. Store DNS provider credentials in OpenBao

cert-manager needs DNS provider credentials to complete the DNS-01 challenge — it creates a temporary `TXT` record to prove you control the domain.

Go to the `common-shared-secret` path in OpenBao and create a secret named `external-dns-creds`.

### Cloudflare

| Key | Required | Description |
|---|---|---|
| `api-token` | Required | API token with `DNS:Edit` and `Zone:Read` permissions |
| `domain-filter` | Optional | Base domain for subdomains, e.g. `example.com` |
| `zone-id-filter` | Optional | Comma-separated Cloudflare zone IDs for restricted access |

---

## 2. Create a Certificate resource via infra GitOps

Deploy two resources to your infra GitOps repository: an ArgoCD Application that tells ArgoCD where to find the certificate, and the `Certificate` resource itself.

### ArgoCD Application

Add this to `CLUSTER_NAME/argocd-apps/certificate-config.yaml`:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: certificate-config
  namespace: rh-openshift-gitops-instance
spec:
  destination:
    namespace: TENANT_SYSTEM_NAMESPACE
    server: https://kubernetes.default.svc
  project: TENANT_NAME
  source:
    path: CLUSTER_NAME/cert-config
    repoURL: INFRA_GITOPS_REPO_URL
    targetRevision: HEAD
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

### Certificate

Add this to `CLUSTER_NAME/cert-config/certificate.yaml`:

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: wildcard-certificate
  namespace: TENANT_SYSTEM_NAMESPACE
spec:
  secretName: TLS_SECRET_NAME
  duration: 8760h0m0s
  renewBefore: 720h0m0s
  dnsNames:
    - '*.example.com'
  issuerRef:
    name: CLUSTER_ISSUER_NAME
    kind: ClusterIssuer
    group: cert-manager.io
```

Replace `*.example.com` with your wildcard domain. Commit and push. ArgoCD deploys the resources within a few minutes — wait for the `Certificate` status to show `Ready` before continuing.

---

## 3. Distribute the certificate across namespaces

The certificate secret is created in the system namespace. To make it available in all tenant namespaces, create a `Template` and `TemplateGroupInstance` in your infra GitOps repository.

Add both to `CLUSTER_NAME/tenant-operator-config/templates/`:

### Template

```yaml
apiVersion: tenantoperator.stakater.com/v1alpha1
kind: Template
metadata:
  name: certificate-template
resources:
  resourceMappings:
    secrets:
      - name: TLS_SECRET_NAME
        namespace: TENANT_SYSTEM_NAMESPACE
```

### TemplateGroupInstance

```yaml
apiVersion: tenantoperator.stakater.com/v1alpha1
kind: TemplateGroupInstance
metadata:
  name: certificate-creds
spec:
  template: certificate-template
  selector:
    matchExpressions:
      - key: stakater.com/tenant
        operator: In
        values:
          - TENANT_NAME
  sync: true
```

Add additional tenant names to `spec.selector.matchExpressions[].values` for any other tenant that needs the certificate. Commit and push — ArgoCD distributes the secret to the selected namespaces within a few minutes.

---

## 4. Validate

1. In the cluster console, switch to **Administrator** view and navigate to **Home > Search**.
1. Select `TENANT_SYSTEM_NAMESPACE` and search for `Certificate` in the **Resources** dropdown.
1. Inspect the certificate and confirm the **Condition** section shows the issuer is up-to-date.

    ![Certificate status](images/certificate-status.png)

1. Confirm the `TLS_SECRET_NAME` secret is present in the target tenant namespaces.

---

With the certificate distributed, you can reference `TLS_SECRET_NAME` in your application's Helm values to enable TLS. See [Configure custom domains](custom-domains.md) for the full end-to-end setup.
