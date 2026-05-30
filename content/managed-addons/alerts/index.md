# Alerts

This page explains how to receive alerts from your application when something goes wrong.

## How it works

Stakater operates a single Alertmanager that handles alerts from both metrics and logs. You declare rules and routing through your application's `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md); the platform evaluates the rules and routes the resulting alerts to the channel you configure. You do not run Alertmanager, configure routing trees, or manage receivers.

The platform also ships a curated set of [predefined PrometheusRules](./predefined-prometheusrules.md) for common Kubernetes failure modes (pod crash-looping, deployment replica mismatch, PVC filling up, and so on). You can route these to your channels — there is no need to write the rules yourself.

## What you do

1. Route alerts from your namespace to a receiver by declaring an `AlertmanagerConfig` through the Application Chart.
1. Optionally declare custom `PrometheusRule` or `AlertingRule` (Loki) resources for conditions the predefined rules do not cover.

Both pieces are scoped to your namespace; Alertmanager merges your routing into its base configuration automatically.

## Next step

Continue to [Configure application alerting](./workload-application-alerts.md) to wire your first alert.
