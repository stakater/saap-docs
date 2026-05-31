# Loki

This page introduces Loki in {{ product_name }} and points you to the logs how-to that uses it.

## How it works

Stakater operates [Loki](https://github.com/grafana/loki) on the cluster as the log aggregation and search layer. Your application emits logs through the OpenTelemetry SDK logs API over OTLP; the in-cluster collector routes them to Loki; you query them in Grafana through Forecastle with LogQL.

## What you do

Instrument your application with the OpenTelemetry SDK and point it at the in-cluster collector via `deployment.env` in your `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md).

## Next step

Continue to [Logs](../logging/index.md) for the full guide.
