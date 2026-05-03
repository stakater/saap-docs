# Configure custom domains

This page explains how to serve your application on your own domain instead of the default cluster URL. The process has four steps: point your DNS to the cluster, provision a TLS certificate, configure your application, and verify the result.

The examples below use `custom.domain.com` as the target domain.

---

## 1. Configure DNS

Point your domain to the cluster's ingress IP address. Contact your cluster administrator to obtain the ingress IP or hostname for your cluster.

Once you have the address, add a DNS `A` record (for a direct IP) or `CNAME` record (for a hostname) in your DNS provider to map `custom.domain.com` to the cluster ingress.

If you want DNS records created automatically when new routes are deployed, see [ExternalDNS](../../managed-addons/external-dns/overview.md).

---

## 2. Configure a TLS certificate

There are two ways to provision a TLS certificate for your domain:

### Option 1: cert-manager (recommended)

Use cert-manager to issue and renew certificates automatically. See [cert-manager managed addon](../../managed-addons/cert-manager/overview.md) for configuration options.

For step-by-step setup using DNS-01 challenges, see [Manage TLS certificates](tls-certs.md).

For HTTP-01 challenges, see [Use HTTP-01 certificate challenges](http01-certs.md).

### Option 2: Bring your own certificate

Generate a TLS certificate for `custom.domain.com` from your preferred CA and create a Kubernetes secret containing it. Then reference the secret in your route:

```yaml
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: my-app-route
  namespace: my-apps-ns
spec:
  host: my-app.custom.domain.com
  path: /
  port:
    targetPort: http
  tls:
    certificate: |
      <base64-encoded certificate>
    key: |
      <base64-encoded key>
    insecureEdgeTerminationPolicy: Redirect
    termination: edge
  to:
    kind: Service
    name: my-app
    weight: 100
  wildcardPolicy: None
```

---

## 3. Configure your application

In your application's Helm values, add an ingress section pointing to your custom domain:

```yaml
ingress:
  enabled: true
  servicePort: <SERVICE_PORT>
  hosts:
  - custom.domain.com
  annotations:
    cert-manager.io/cluster-issuer: ca-issuer
  tls:
  - hosts:
    - custom.domain.com
    secretName: custom-domain-tls-cert
```

cert-manager will issue the certificate within 2–3 minutes. The `custom-domain-tls-cert` secret is populated automatically once the certificate is ready.

---

## 4. Verify

Once the certificate is issued and the route is created, open `https://custom.domain.com` in a browser to confirm your application is reachable over TLS.

---

For DNS-01 wildcard certificate setup, continue to [Manage TLS certificates](tls-certs.md).
