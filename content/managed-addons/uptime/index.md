# Uptime

This page shows you how to add external uptime checks for your application's public endpoints.

## How it works

{{ product_name }} runs external uptime probes against your public endpoints using Ingress Monitor Controller (IMC) and UptimeRobot. Both are fully managed by Stakater — IMC is configured against UptimeRobot for you, and the probes run from outside the cluster so they catch outages that internal monitoring would miss.

You do not configure IMC, manage API credentials, or create UptimeRobot monitors by hand. You enable uptime monitoring through your application's `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md), and IMC registers the matching monitor in UptimeRobot for you.

## What you do

1. Enable `endpointMonitor` in the Application Chart `values.yaml` for the application you want monitored. The chart generates an `EndpointMonitor` that points at the application's Route or Ingress.
1. Provide Stakater Support with the Slack webhook (or other contact) where you want downtime alerts delivered. Stakater registers it as an UptimeRobot alert contact for your monitors.

That is the full setup — IMC reconciles the rest.

## Next step

Continue to [Add an EndpointMonitor](./add-monitors.md) to enable monitoring for your first application.
