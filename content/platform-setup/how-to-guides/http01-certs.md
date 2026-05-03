# Use http-01 certificate challenges

This guide explains how to issue a TLS certificate for a specific hostname using cert-manager's http-01 challenge.

Use this approach when your cluster is publicly reachable from the internet and you need a certificate for a single hostname. cert-manager proves you control the domain by serving a temporary file over http — no DNS provider credentials required. For wildcard certificates or clusters without public internet access, use [DNS-01 challenges](tls-certs.md) instead.

**Prerequisites:**

- A `ClusterIssuer` is configured on your cluster. Confirm the name with your cluster administrator before starting.
- The hostname you want to secure must resolve to the cluster's ingress IP address before you begin.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `HOSTNAME` | The hostname to secure (e.g. `app.example.com`) |
| `CERT_NAME` | A name for the `Certificate` resource |
| `TLS_SECRET_NAME` | The name of the Kubernetes secret cert-manager will create |
| `CLUSTER_ISSUER_NAME` | The name of the `ClusterIssuer` on your cluster |
| `APP_NAMESPACE` | The namespace where your application runs |
| `ROUTE_NAME` | A name for the OpenShift `Route` resource |
| `SERVICE_NAME` | The name of the Kubernetes `Service` to route traffic to |

---

## 1. Create a DNS record

Add an `A` record (for a direct IP) or `CNAME` record (for a hostname) in your DNS provider that maps `HOSTNAME` to the cluster's ingress address. Contact your cluster administrator if you do not have the ingress address.

cert-manager will attempt the challenge immediately after the `Certificate` resource is created, so the DNS record must be live before you proceed.

---

## 2. Deploy the Certificate and Route

Add both resources to your application's Helm chart under `templates/`:

### Certificate

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: CERT_NAME
  namespace: APP_NAMESPACE
spec:
  secretName: TLS_SECRET_NAME
  issuerRef:
    name: CLUSTER_ISSUER_NAME
    kind: ClusterIssuer
  commonName: HOSTNAME
  dnsNames:
    - HOSTNAME
```

!!! note
    Avoid deleting or recrereating certificates unnecessarily. Repeated issuance attempts count against [Let's Encrypt rate limits](https://letsencrypt.org/docs/rate-limits/).

### Route

```yaml
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: ROUTE_NAME
  namespace: APP_NAMESPACE
  annotations:
    cert-utils-operator.redhat-cop.io/certs-from-secret: TLS_SECRET_NAME
    cert-utils-operator.redhat-cop.io/inject-CA: "false"
spec:
  host: HOSTNAME
  path: /
  port:
    targetPort: http
  to:
    kind: Service
    name: SERVICE_NAME
    weight: 100
  wildcardPolicy: None
  tls:
    termination: edge
    insecureEdgeTerminationPolicy: Redirect
```

The `cert-utils-operator` annotation injects the certificate from `TLS_SECRET_NAME` into the route automatically once cert-manager issues it.

---

## 3. Validate

### Certificate

1. In the cluster console, switch to **Administrator** view and navigate to **Home > Search**.
1. Select `APP_NAMESPACE` and search for `Certificate` in the **Resources** dropdown.
1. Inspect the certificate and confirm the **Condition** shows it is up-to-date.

    ![Certificate status](images/certificate-status.png)

### Route

1. Navigate to **Networking > Routes** in the cluster console.
1. Locate `ROUTE_NAME` and confirm its status is **Accepted**.
1. Open `https://HOSTNAME` in a browser to confirm the certificate is valid and the application is reachable.

---

With TLS configured, your application is reachable over https on its custom hostname. See [Configure custom domains](custom-domains.md) for the full end-to-end setup including DNS and application-level configuration.
