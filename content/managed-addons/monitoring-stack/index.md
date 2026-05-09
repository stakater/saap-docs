# Observe

{{ product_name }} provides a unified observability stack based on the LGTM suite — Grafana, Mimir, Loki, and Tempo — giving you metrics, logs, traces, and uptime monitoring in a single, integrated experience.

All observability signals are accessible through the Grafana dashboard in Forecastle.

---

## Metrics & Alerts

Metrics are scraped by Prometheus and stored in Mimir. Define `ServiceMonitor` resources to scrape your application endpoints, and `PrometheusRule` resources to fire alerts based on those metrics. Alertmanager routes and deduplicates alerts before delivering them to your notification channels.

## Logs

Application logs written to stdout are captured automatically by Vector, aggregated in Loki, and queryable through Grafana's Explore view. No configuration is required to start collecting logs.

## Traces

Distributed traces are collected via the OpenTelemetry Collector and stored in Tempo. Instrument your application with an OpenTelemetry SDK to emit spans and correlate requests across services.

## Uptime

Ingress Monitor Controller watches your Routes and Ingresses and automatically registers external uptime checks. You receive an alert when a public endpoint goes down.
