# Logs

{{ product_name }} captures all application logs written to stdout automatically. Logs are collected by Vector, aggregated in Loki, and queryable through Grafana's Explore view.

No configuration is required to start collecting logs — any workload running on the platform has its stdout and stderr captured and indexed. Filter and search by namespace, pod, or label directly in Grafana.

---

- [Log alerts](../monitoring-stack/log-alerts.md) — receive Slack alerts when error patterns appear in your application logs
