# Expose your application over https

This guide explains how to configure an OpenShift `Route` to serve your application on a custom hostname over https using a TLS certificate managed by cert-manager.

**Prerequisites:**

- A `Certificate` resource is configured in your cluster. Confirm the secret name with your cluster administrator.
- ExternalDNS is operational and will register the DNS record automatically when the `Route` is created.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `TLS_SECRET_NAME` | The name of the Kubernetes secret holding the TLS certificate |
| `HOSTNAME` | The custom hostname for your application (e.g. `app.example.com`) |
| `APP_PATH` | The URL path to expose (e.g. `/` or `/api`) |

---

## 1. Update your Helm values

Add a `route` section to your application's `values.yaml`:

```yaml
application:
  route:
    enabled: true
    annotations:
      cert-utils-operator.redhat-cop.io/certs-from-secret: TLS_SECRET_NAME
      external-dns.alpha.kubernetes.io/hostname: HOSTNAME
      cert-utils-operator.redhat-cop.io/inject-CA: "false"
    host: HOSTNAME
    path: APP_PATH
```

The `cert-utils-operator` annotation injects the TLS certificate from `TLS_SECRET_NAME` into the route automatically. The `external-dns` annotation registers the DNS record with your configured DNS provider.

---

## 2. Verify

Commit and push your changes. After ArgoCD syncs:

1. Navigate to **Networking > Routes** in the OpenShift console.
1. Locate the route for your application.
1. Confirm the status is **Accepted** and the hostname and TLS settings are correct.
1. Open `https://HOSTNAME` in a browser to confirm the application is reachable.

---

For wildcard certificates or custom TLS setup, see [Configure TLS certificates](../../../platform-setup/how-to-guides/tls-certs.md).
