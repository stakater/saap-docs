# Traces

This page shows you how to send distributed traces from your application to {{ product_name }} and explore them in Grafana.

## How it works

Stakater operates Tempo for trace storage and Grafana for visualization. Your application emits spans through the OpenTelemetry SDK; the SDK exports OTLP to the in-cluster collector; the collector routes them to Tempo; you query them in Grafana through Forecastle. Trace context is propagated across services so a single request shows up as one end-to-end trace.

## What you do

Add the OpenTelemetry SDK or auto-instrumentation agent for your language to your application, then set the OTel SDK environment variables on your pod via `deployment.env` in your `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md):

```yaml
deployment:
  env:
    - name: OTEL_SERVICE_NAME
      value: your-service-name
    - name: OTEL_EXPORTER_OTLP_ENDPOINT
      value: http://otel-collector.observability.svc.cluster.local:4317
    - name: OTEL_TRACES_EXPORTER
      value: otlp
```

For Java, Python, Node.js, and .NET, the auto-instrumentation agent captures web request, database, and messaging spans without code changes. Open Grafana from Forecastle, switch to Explore, select the Tempo data source, and search by trace ID, service name, or duration. From a trace you can jump to the matching logs in Loki or metrics in Mimir.

## Next step

Continue to [Dashboards](../dashboards/index.md) to build a Grafana dashboard that combines metrics, logs, and traces.
