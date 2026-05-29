# Logs

This page shows you how to send your application logs to {{ product_name }} and search them in Grafana.

## How it works

Stakater operates Loki for log storage and Grafana for querying. Your application emits logs through the OpenTelemetry SDK logs API; the SDK exports OTLP to the in-cluster collector; the collector routes them to Loki; you query them in Grafana through Forecastle.

## What you do

Set the OTel SDK environment variables on your pod via `deployment.env` in your application's `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md) — the same block you use for metrics and traces, since the OTel collector accepts all three signals on the same endpoint:

```yaml
deployment:
  env:
    - name: OTEL_SERVICE_NAME
      value: your-service-name
    - name: OTEL_EXPORTER_OTLP_ENDPOINT
      value: http://otel-collector.observability.svc.cluster.local:4317
    - name: OTEL_LOGS_EXPORTER
      value: otlp
```

Structured log attributes (severity, trace context, custom fields) are preserved in Loki. Open Grafana from Forecastle, switch to Explore, select the Loki data source, and filter with LogQL:

```logql
{namespace="your-namespace"} |= "ERROR"
```

For JSON logs, pipe through the `json` parser and match on individual fields:

```logql
{namespace="your-namespace"} | json | level="error"
```

## Next step

Continue to [Alerts](../alerts/index.md) to fire alerts when an error pattern appears in your logs.
