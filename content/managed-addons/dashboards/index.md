# Dashboards

This page shows you how to ship a Grafana dashboard for your application through the [Stakater Application Helm Chart](../helm-leader-chart/index.md).

## How it works

Stakater operates Grafana and the Grafana Operator on the cluster. You declare dashboards through your application's `values.yaml`; the chart renders the matching `GrafanaDashboard` resource; the operator registers it in Grafana automatically. You do not log into Grafana to import dashboards by hand, and you do not need cluster-admin access — the same chart commit ships the dashboard to every environment.

## What you do

Build the dashboard interactively in Grafana first, then export the JSON. Add it to your `values.yaml` under `grafanaDashboard`:

```yaml
grafanaDashboard:
  enabled: true
  contents:
    example-dashboard:
      json: |-
        {
          "title": "Example dashboard",
          "panels": [],
          "schemaVersion": 27
        }
```

The chart applies the required `grafanaDashboard: grafana-operator` label and places the dashboard in a Grafana folder named after your namespace. Open Grafana from Forecastle and navigate to **Dashboards → Browse** to find it. If the JSON is invalid, the dashboard does not appear — check the operator's logs.

## Next step

Continue to [Uptime](../uptime/index.md) to add external availability checks for your application.
