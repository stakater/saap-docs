# Configure secure routes

This guide explains how to expose your application over https using an OpenShift Route configured through the [Stakater Application Chart](https://github.com/stakater/application).

{{ product_name }} provisions every cluster with a wildcard domain in the format `*.apps.CLUSTER_NAME.CLUSTER_ID.kubeapp.cloud`, pre-configured with edge TLS termination. Any route using this domain is already secured — no additional certificate setup required.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `APP_NAME` | Your application name |
| `APP_HOSTNAME` | A custom hostname for the route (optional — if omitted, OpenShift generates one from the cluster domain) |
| `ALLOWLISTED_IPS` | Space-separated list of IPs allowed to access the route (for IP restriction) |

---

## 1. Enable the route

In your application's `deploy/values.yaml`, add a `route` section under `application`:

```yaml
application:
  route:
    enabled: true
    port:
      targetPort: http
    tls:
      termination: edge
      insecureEdgeTerminationPolicy: Redirect
```

When `host` is omitted, OpenShift automatically assigns a hostname using the cluster's wildcard domain. This is the simplest and most common configuration.

---

## 2. Set a custom hostname (optional)

To use a specific hostname instead of the auto-generated one, add a `host` field:

```yaml
application:
  route:
    enabled: true
    host: APP_HOSTNAME
    port:
      targetPort: http
    tls:
      termination: edge
      insecureEdgeTerminationPolicy: Redirect
```

!!! note
    A custom hostname requires a DNS record pointing to the cluster ingress and a matching TLS certificate. See [Configure custom domains](../platform-setup/how-to-guides/custom-domains.md) for the full setup.

---

## 3. Restrict access by IP (optional)

To allow traffic only from specific IP addresses, add the `ip_whitelist` annotation:

```yaml
application:
  route:
    enabled: true
    port:
      targetPort: http
    tls:
      termination: edge
      insecureEdgeTerminationPolicy: Redirect
    annotations:
      haproxy.router.openshift.io/ip_whitelist: "ALLOWLISTED_IPS"
```

Separate multiple IPs with spaces: `"10.0.0.1 10.0.0.2 203.0.113.5"`.

---

## 4. Set a custom timeout (optional)

To override the default server-side timeout, add the `timeout` annotation:

```yaml
application:
  route:
    enabled: true
    port:
      targetPort: http
    tls:
      termination: edge
      insecureEdgeTerminationPolicy: Redirect
    annotations:
      haproxy.router.openshift.io/timeout: 5000ms
```

---

## 5. Verify

Commit and push your `values.yaml` changes. ArgoCD will apply the route within a few minutes.

In the OpenShift console, navigate to **Networking > Routes** in your application namespace. Confirm the route is listed, its status is **Accepted**, and the lock icon indicates a secure connection.

---

For path-based routing or URL rewriting, see [Rewrite request paths](../develop/how-to-guides/rewriting-path-annotation/path-rewriting.md). For exposing on a custom domain with cert-manager, see [Expose your application over https](../develop/how-to-guides/expose-applications-to-internet/expose-applications-to-internet.md).
