# Observe

This section shows you how to set up metrics, alerts, logs, traces, dashboards, and uptime monitoring for your application on {{ product_name }}.

## How it works

{{ product_name }} runs a fully managed observability stack on your behalf — Grafana, Mimir, Loki, Tempo, Alertmanager, the OpenTelemetry collector, Ingress Monitor Controller, and the UptimeRobot integration. You do not install, configure, scale, or upgrade any of these components.

Signals (metrics, logs, traces) are emitted by your application via the OpenTelemetry SDK over OTLP. Alerts, dashboards, and uptime monitors are declared through your application's `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md) and shipped via GitOps. There is exactly one supported way for each — Prometheus scraping, Fluentd, Micrometer/Actuator, direct stdout shipping, and hand-written CRDs are not part of the platform's supported surface.

## What you do

| Capability | What you do |
|------------|-------------|
| [Metrics](../metrics/index.md) | Emit metrics over OTLP from the OpenTelemetry SDK; query them in Grafana with PromQL. |
| [Alerts](../alerts/index.md) | Declare `PrometheusRule`, `AlertingRule`, and `AlertmanagerConfig` through your `values.yaml` to fire and route alerts. |
| [Logs](../logging/index.md) | Emit logs over OTLP from the OpenTelemetry SDK; search them in Grafana with LogQL. |
| [Traces](../tracing/index.md) | Emit spans over OTLP from the OpenTelemetry SDK; correlate requests across services in Tempo. |
| [Dashboards](../dashboards/index.md) | Declare `grafanaDashboard` contents in your `values.yaml` to ship Grafana dashboards via GitOps. |
| [Uptime](../uptime/index.md) | Enable `endpointMonitor` in your `values.yaml` to register external uptime probes via UptimeRobot. |

## Next step

Continue to [Metrics](../metrics/index.md) to instrument your first application.
