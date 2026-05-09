# Configure application alerting

This guide explains how to configure metrics scraping, alert routing, and alert rules for your application using the Stakater Application Helm Chart.

1. [Create a ServiceMonitor](#1-create-a-servicemonitor) — tell Prometheus which endpoint to scrape
1. [Create an AlertmanagerConfig](#2-create-an-alertmanagerconfig) — route alerts to Slack, PagerDuty, or another target
1. [Create a PrometheusRule](#3-optional-create-a-prometheusrule) (optional) — define custom alert thresholds

---

## 1. Create a ServiceMonitor

A `ServiceMonitor` tells Prometheus which endpoint on your application to scrape for metrics. Enable it in your `values.yaml`:

| Parameter | Description |
|:---|:---|
| `application.serviceMonitor.enabled` | Enable `ServiceMonitor` |
| `application.serviceMonitor.endpoints` | Array of endpoints to be scraped by Prometheus |

```yaml
application:
  serviceMonitor:
    enabled: true
    endpoints:
      - interval: 5s
        path: /actuator/prometheus
        port: http
```

---

## 2. Create an AlertmanagerConfig

An `AlertmanagerConfig` routes alerts to a notification target. This example routes to a Slack channel.

**Step 1:** Create a secret containing the Slack webhook URL:

```yaml
kind: Secret
apiVersion: v1
metadata:
  name: slack-webhook-config
  namespace: YOUR_NAMESPACE
data:
  webhook-url: SLACK_WEBHOOK_URL_BASE64
type: Opaque
```

**Step 2:** Configure the `AlertmanagerConfig` in your `values.yaml`. Replace `ALERTMANAGER_URL` with the Workload Alertmanager URL from Forecastle.

| Parameter | Description |
|:---|:---|
| `application.alertmanagerConfig.enabled` | Enable AlertmanagerConfig (merged into the base Alertmanager config) |
| `application.alertmanagerConfig.spec.route` | Alertmanager route definition for alerts matching the resource's namespace |
| `application.alertmanagerConfig.spec.receivers` | List of receivers |

<!-- vale off -->
{% raw %}

```yaml
application:
  alertmanagerConfig:
    enabled: true
    spec:
      route:
        receiver: 'slack-webhook'
      receivers:
        - name: 'slack-webhook'
          slackConfigs:
            - apiURL:
                name: slack-webhook-config
                key: webhook-url
              channel: '#CHANNEL_NAME'
              sendResolved: true
              text: |2-
                {{ range .Alerts }}
                *Alert:* `{{ .Labels.severity | toUpper }}` - {{ .Annotations.summary }}
                *Description:* {{ .Annotations.description }}
                *Details:*
                  {{ range .Labels.SortedPairs }} *{{ .Name }}:* `{{ .Value }}`
                  {{ end }}
                {{ end }}
              title: '[{{ .Status | toUpper }}{{ if eq .Status "firing" }}:{{ .Alerts.Firing | len }}{{ end }}] {% endraw %}{{ product_name }}{% raw %} Alertmanager Event Notification'
              titleLink: |2
                ALERTMANAGER_URL/#/alerts?receiver={{ .Receiver | urlquery }}
              httpConfig:
                tlsConfig:
                  insecureSkipVerify: true
```

{% endraw %}
<!-- vale on -->

Alertmanager automatically scopes alerts to the deploying namespace by adding a `namespace` match.

---

## 3. [Optional] Create a PrometheusRule

{{ product_name }} ships with [predefined PrometheusRules](./predefined-prometheusrules.md) that cover common scenarios. Define a custom rule only when the predefined ones do not cover your use case.

| Parameter | Description |
|:---|:---|
| `application.prometheusRule.enabled` | Enable PrometheusRule for this app |
| `application.prometheusRule.groups` | PrometheusRule groups to be added |

```yaml
application:
  prometheusRule:
    enabled: true
    groups:
      - name: example-app-uptime
        rules:
          - alert: ExampleAppDown
            annotations:
              message: >-
                The Example App is Down (Test Alert)
            expr: up{namespace="test-app"} == 0
            for: 1m
            labels:
              severity: critical
```
