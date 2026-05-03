# Rewrite request paths

This guide explains how to configure path rewriting on an OpenShift Route using the [Stakater Application Chart](https://github.com/stakater/application).

Use path rewriting when your application serves traffic from one path internally but you need to expose it at a different path externally. For example, your backend serves from `/` but you want external traffic to arrive at `/api`.

Replace the following placeholders with your own values throughout this guide:

| Placeholder | Description |
|---|---|
| `APP_HOSTNAME` | The hostname for your route |
| `EXTERNAL_PATH` | The path exposed externally (e.g. `/api`) |
| `BACKEND_PATH` | The path the backend expects to receive (e.g. `/`) |

---

## 1. Configure path rewriting in your values

In your application's `deploy/values.yaml`, add the `rewrite-target` annotation and set `path` to the external path you want to expose:

```yaml
application:
  route:
    enabled: true
    host: APP_HOSTNAME
    path: EXTERNAL_PATH
    port:
      targetPort: http
    tls:
      termination: edge
      insecureEdgeTerminationPolicy: Redirect
    annotations:
      haproxy.router.openshift.io/rewrite-target: BACKEND_PATH
```

With this configuration, a request arriving at `https://APP_HOSTNAME/EXTERNAL_PATH/foo` is rewritten to `BACKEND_PATH/foo` before reaching your container.

---

## 2. Verify

Commit and push your changes. After ArgoCD syncs, confirm the route in the OpenShift console under **Networking > Routes**.

Send a request to the external path and confirm your application responds correctly:

```bash
curl https://APP_HOSTNAME/EXTERNAL_PATH
```

---

For securing a route with IP restrictions or custom timeouts, see [Configure secure routes](../../../operate/secure-routes.md). For exposing on a custom domain with a cert-manager certificate, see [Expose your application over HTTPS](../expose-applications-to-internet/expose-applications-to-internet.md).
