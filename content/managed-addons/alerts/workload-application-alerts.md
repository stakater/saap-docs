# Configure application alerting

This guide shows you how to route alerts from your application to Slack and how to declare a custom alert rule.

## How it works

The platform already ingests your metrics through OpenTelemetry, so you do not configure scraping to receive alerts. You declare where alerts should go through an `AlertmanagerConfig` in your `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md); predefined PrometheusRules fire against your workloads automatically. Optionally, declare a custom `PrometheusRule` for conditions the predefined ones do not cover.

## 1. Route alerts to Slack

Create a Secret containing the Slack webhook URL:

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

Enable the `AlertmanagerConfig` in your `values.yaml`. The Workload Alertmanager URL used in `titleLink` is available from Forecastle.

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

Alertmanager scopes alerts to your namespace automatically by adding a `namespace` match. Once routing is in place, any predefined PrometheusRule that fires for your workloads — and any custom rule you declare below — lands in your Slack channel.

## 2. Declare a custom alert rule

Declare a custom rule only when you need a condition the [predefined rules](./predefined-prometheusrules.md) do not cover — for example, a business metric specific to your application.

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

The rule is evaluated by the platform's Mimir ruler. When it fires, the alert flows through the same Alertmanager routing you configured in step 1.

## Next step

Continue to [Predefined PrometheusRules](./predefined-prometheusrules.md) to see what alerts you already get out of the box.
