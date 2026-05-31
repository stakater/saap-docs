# Mimir

This page introduces Mimir in {{ product_name }} and points you to the metrics how-to that uses it.

## How it works

Stakater operates [Mimir](https://github.com/grafana/mimir) on the cluster as the long-term metrics store. Your application emits metrics through the OpenTelemetry SDK over OTLP; the in-cluster OpenTelemetry collector routes them to Mimir; you query them in Grafana through Forecastle with PromQL.

## What you do

Instrument your application with the OpenTelemetry SDK and point it at the in-cluster collector via `deployment.env` in your `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md).

## Next step

Continue to [Metrics](../metrics/index.md) for the full guide.
