# Configure TLS certificates

This page explains how to provision a wildcard TLS certificate using cert-manager with a DNS-01 challenge, distribute it across tenant namespaces, and validate the result. Use this approach when you need wildcard coverage (e.g. `*.example.com`) or when your cluster is not publicly reachable.

For http-01 challenges (no DNS credentials required), see [Use http-01 certificate challenges](http01-certs.md).

---

## 1. Store DNS provider credentials in OpenBao

Go to the `common-shared-secret` path in OpenBao and create a secret named `external-dns-creds`. This secret holds the credentials cert-manager uses to complete the DNS-01 challenge.

### Cloudflare

| Key | Required | Description |
|---|---|---|
| `api-token` | Required | API token with `DNS:Edit` and `Zone:Read` permissions |
| `domain-filter` | Optional | Base domain for subdomains, e.g. `example.com` |
| `zone-id-filter` | Optional | Comma-separated Cloudflare zone IDs for restricted access |

!!! note
    Before proceeding, confirm with your cluster administrator that a `ClusterIssuer` is set up. The next steps depend on it.

---

## 2. Create a Certificate resource via infra GitOps

Deploy the following two resources to your infra GitOps repository.

### ArgoCD application

Path: `<cluster>/argocd-apps/`

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: certificate-config
  namespace: rh-openshift-gitops-instance
spec:
  destination:
    namespace: <tenant-system-namespace>
    server: https://kubernetes.default.svc
  project: <tenant-name>
  source:
    path: <cluster>/<path-to-certificate-folder>
    repoURL: <infra-gitops-repo-url>
    targetRevision: HEAD
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

Key fields:

- **`.spec.destination.namespace`** — The tenant's system namespace. Confirm availability with your cluster administrator.
- **`.spec.project`** — The ArgoCD project (usually the tenant name).
- **`.spec.source.path`** — The folder in your infra GitOps repo containing the `Certificate` resource.

### Certificate

Path: `<cluster>/<path-to-certificate-folder>/`

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: certificate
spec:
  secretName: <tls-secret-name>
  duration: 8760h0m0s
  renewBefore: 720h0m0s
  dnsNames:
    - '*.example.com'
  issuerRef:
    name: <cluster-issuer-name>
    kind: ClusterIssuer
    group: cert-manager.io
```

Key fields:

- **`.spec.secretName`** — The Kubernetes secret cert-manager creates once the certificate is issued.
- **`.spec.dnsNames`** — DNS names the certificate covers. Wildcard names like `*.example.com` are supported.
- **`.spec.issuerRef.name`** — The `ClusterIssuer` name. Confirm the value with your cluster administrator.

Commit and push. ArgoCD deploys the resources within a few minutes. Verify that the certificate appears in the system namespace and its status shows `Ready` before continuing.

---

## 3. Distribute the certificate across namespaces

To make the TLS secret available in all tenant namespaces, create a `Template` and `TemplateGroupInstance` in your infra GitOps repository.

Path: `<cluster>/tenant-operator-config/templates/`

### Template

```yaml
apiVersion: tenantoperator.stakater.com/v1alpha1
kind: Template
metadata:
  name: certificate-template
resources:
  resourceMappings:
    secrets:
      - name: <tls-secret-name>
        namespace: <system-namespace>
```

Key fields:

- **`.resources.resourceMappings.secrets[].name`** — The secret cert-manager created in the system namespace.
- **`.resources.resourceMappings.secrets[].namespace`** — The system namespace where the certificate lives.

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
          - <tenant-name>
  sync: true
```

Key fields:

- **`.spec.template`** — References the `Template` above.
- **`.spec.selector`** — Targets namespaces by tenant label. Add all tenants that need the certificate.

Commit and push. ArgoCD distributes the secret to the selected namespaces within a few minutes.

---

## 4. Validate

1. In the cluster console, switch to **Administrator** view and navigate to **Home > Search**.
1. Select the system namespace and search for `Certificate` in the **Resources** dropdown.
1. Inspect the certificate. In the **Condition** section, confirm the issuer is up-to-date.

    ![Certificate status](images/certificate-status.png)

1. Confirm the TLS secret is present in the target tenant namespaces.
