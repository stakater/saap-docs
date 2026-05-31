# IngressMonitorController

This page introduces Ingress Monitor Controller (IMC) in {{ product_name }} and points you to the uptime how-to that uses it.

## How it works

Stakater operates [IMC](https://github.com/stakater/IngressMonitorController) on the cluster, configured against UptimeRobot for you. It watches `EndpointMonitor` resources that you declare through the [Stakater Application Helm Chart](../helm-leader-chart/index.md) and registers matching external uptime monitors in UptimeRobot. Probes run from outside the cluster so they catch outages that internal monitoring would miss.

## What you do

Enable `endpointMonitor` in your application's `values.yaml`. The chart generates the `EndpointMonitor` resource for the Route or Ingress your application already declares; IMC reconciles it; probing starts within a couple of minutes.

## Next step

Continue to [Uptime](../uptime/index.md) for the full guide.
