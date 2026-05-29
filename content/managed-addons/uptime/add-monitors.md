# Add an EndpointMonitor

This guide shows you how to enable external uptime monitoring for your application using the [Stakater Application Helm Chart](../helm-leader-chart/index.md).

## How it works

The chart reads the Route or Ingress already declared in your `values.yaml`, generates a matching `EndpointMonitor` resource, and ships it through GitOps. IMC reconciles the resource into UptimeRobot and external probing starts within a couple of minutes — no API keys, no manual UptimeRobot setup.

## What you do

Enable `endpointMonitor` in your application's `values.yaml`:

```yaml
endpointMonitor:
  enabled: true
```

To force a secure connection or override the monitor name, extend the same block:

```yaml
endpointMonitor:
  enabled: true
  forceHttps: true
  name: my-app-frontend
```

See the chart's [`endpointmonitor.yaml` template](https://github.com/stakater/application/blob/master/application/templates/endpointmonitor.yaml) for the full set of supported fields.

## Next step

Continue to [Downtime notifications](./downtime-notifications.md) to route downtime alerts to your Slack channel.
