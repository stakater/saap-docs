# Uptime Monitoring

Ingress Monitor Controller watches Routes and Ingresses in the cluster and automatically registers external uptime checks via UptimeRobot. When a monitored endpoint goes down, an alert is sent to your configured notification channel.

Enable uptime monitoring for an application by adding an `EndpointMonitor` resource, or by enabling `endpointMonitor` in the Stakater Application Helm Chart.

---

- [Add configuration](./tutorial/add-configuration.md) — configure IMC with your UptimeRobot API credentials
- [Add an EndpointMonitor](./tutorial/add-monitors.md) — register a URL, route, or ingress for uptime monitoring
- [Downtime notifications](../monitoring-stack/downtime-notifications-uptimerobot.md) — route downtime alerts to a Slack channel
