# OpenTelemetry

This page explains how OpenTelemetry fits into {{ product_name }} and where to go to instrument each signal.

## How it works

{{ product_name }} standardizes on OpenTelemetry as the single instrumentation path for application observability. Stakater operates the OpenTelemetry Collector, which accepts metrics, logs, and traces over OTLP at one in-cluster endpoint and routes them to Mimir, Loki, and Tempo automatically.

## What you do

Add the OpenTelemetry SDK for your language to your application and point it at the in-cluster collector:

```bash
OTEL_EXPORTER_OTLP_ENDPOINT=http://otel-collector.observability.svc.cluster.local:4317
```

The same endpoint accepts all three signals. Configure metrics, logs, and traces individually following the signal-specific pages below.

| Signal | How to instrument |
|--------|--------------------|
| [Metrics](../metrics/index.md) | Emit counters, gauges, and histograms over OTLP. |
| [Logs](../logging/index.md) | Forward structured logs to Loki via OTLP. |
| [Traces](../tracing/index.md) | Emit distributed traces to Tempo via OTLP. |

## Next step

Continue to [Metrics](../metrics/index.md) to instrument your first signal.
