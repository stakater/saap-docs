# Stakater Application Helm Chart

The [Stakater Application Helm Chart](https://github.com/stakater/application) is the standard way to deploy any application on the platform. It packages all the Kubernetes resources a typical workload needs — Deployment, Service, Route, HPA, PDB, ServiceMonitor, ConfigMap, ExternalSecret — into a single chart configured entirely through `values.yaml`.

This replaces writing raw Kubernetes manifests for each resource. Every application on the platform uses the same chart structure, making deployment configuration consistent and reviewable across teams.

---

## What the chart manages

All resources are opt-in and disabled by default. Enable only what your application needs:

| Resource | Values key |
|---|---|
| Deployment | `application.deployment` |
| Service | `application.service` |
| Route / Ingress | `application.route` |
| Horizontal Pod Autoscaler | `application.hpa` |
| Pod Disruption Budget | `application.pdb` |
| ServiceMonitor | `application.serviceMonitor` |
| ConfigMap | `application.configMap` |
| ExternalSecret | `application.externalSecret` |
| Forecastle entry | `application.forecastle` |

---

## Add it as a dependency

In your application's `Chart.yaml`:

```yaml
dependencies:
  - name: application
    version: 2.1.13
    repository: https://stakater.github.io/stakater-charts
```

Then configure it in `values.yaml`:

```yaml
application:
  deployment:
    image:
      repository: HARBOR_REGISTRY_URL/TENANT_NAME/APP_NAME
      tag: IMAGE_TAG
  service:
    enabled: true
    ports:
      - port: 8080
        name: http
  route:
    enabled: true
    port:
      targetPort: http
```

For the complete values reference, see the [chart repository](https://github.com/stakater/application).
