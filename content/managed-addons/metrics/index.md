# Metrics

This page explains how to send your application's metrics to {{ product_name }} and view them in Grafana.

## How it works

Stakater operates the OpenTelemetry collector, Mimir for storage, and Grafana for visualization. Your application emits metrics through the OpenTelemetry SDK; the SDK exports OTLP to the in-cluster collector; the collector routes them to Mimir; you query them in Grafana through Forecastle.

## What you do

Set the OTel SDK environment variables on your pod via `deployment.env` in your application's `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md):

```yaml
deployment:
  env:
    - name: OTEL_SERVICE_NAME
      value: your-service-name
    - name: OTEL_EXPORTER_OTLP_ENDPOINT
      value: http://otel-collector.observability.svc.cluster.local:4317
    - name: OTEL_METRICS_EXPORTER
      value: otlp
```

The in-cluster endpoint is reachable from every workload on the cluster. No authentication is required — the platform isolates metrics by namespace automatically. Open Grafana from Forecastle and use the Explore view to query your metrics with PromQL.

## Next step

Continue to [Expose metrics from a Spring Boot application](../../develop/how-to-guides/expose-spring-boot-metrics/expose-spring-boot-metrics.md) for a worked example.
