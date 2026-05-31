# Tempo

This page introduces Tempo in {{ product_name }} and points you to the traces how-to that uses it.

## How it works

Stakater operates [Tempo](https://github.com/grafana/tempo) on the cluster as the distributed tracing backend. Your application emits spans through the OpenTelemetry SDK over OTLP; the in-cluster collector routes them to Tempo; you query them in Grafana through Forecastle by trace ID, service, or duration.

## What you do

Instrument your application with the OpenTelemetry SDK or auto-instrumentation agent for your language, and point it at the in-cluster collector via `deployment.env` in your `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md).

## Next step

Continue to [Traces](../tracing/index.md) for the full guide.
