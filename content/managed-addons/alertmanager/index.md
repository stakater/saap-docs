# Alertmanager

This page introduces Alertmanager in {{ product_name }} and points you to the alerts how-to that uses it.

## How it works

Stakater operates a single [Alertmanager](https://github.com/prometheus/alertmanager) on the cluster that handles alerts from both metrics (Mimir) and logs (Loki). You declare alert rules and routing in your application's `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md); Alertmanager merges your routing into its base configuration and delivers alerts to Slack, PagerDuty, email, or any other configured receiver.

## What you do

Declare an `AlertmanagerConfig` for routing and, optionally, `PrometheusRule` or `AlertingRule` resources for custom conditions. The platform also ships predefined PrometheusRules for common Kubernetes failure modes — you route those without writing the rules yourself.

## Next step

Continue to [Alerts](../alerts/index.md) for the full guide.
