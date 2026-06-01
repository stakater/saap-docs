# Grafana

This page introduces Grafana in {{ product_name }} and points you to the how-tos that use it.

## How it works

Stakater operates [Grafana](https://github.com/grafana/grafana) on the cluster as the visualization layer for metrics, logs, and traces. You access it through [Forecastle](../forecastle/index.md); it queries metrics from Mimir, logs from Loki, and traces from Tempo, and renders dashboards you declare in your application's `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md).

## What you do

Ship dashboards for your applications through GitOps. The chart renders the `GrafanaDashboard` resource and the Grafana Operator registers the dashboard automatically — no manual import.

## Next step

Continue to [Dashboards](../dashboards/index.md) for the full guide.
