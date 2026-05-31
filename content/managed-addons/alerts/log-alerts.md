# Log alerts

This guide shows you how to fire an alert when an error pattern appears in your application logs.

## How it works

The platform's Loki ruler evaluates log-based alert rules against the logs you forward to Loki and sends matching alerts to the same Alertmanager that handles your metric alerts. Routing — Slack, PagerDuty, email — is configured once with an `AlertmanagerConfig` (see [Configure application alerting](./workload-application-alerts.md)) and applies to both signal types.

## What you do

Declare an `AlertingRule` in your namespace. The example below fires when log lines from your namespace contain `ERROR` more than five times per second over five minutes:

```yaml
apiVersion: loki.grafana.com/v1
kind: AlertingRule
metadata:
  name: high-error-rate
  namespace: YOUR_NAMESPACE
spec:
  tenantID: application
  groups:
    - name: error-rate
      rules:
        - alert: HighApplicationErrorRate
          expr: |
            sum(rate({namespace="YOUR_NAMESPACE"} |= "ERROR" [5m])) > 5
          for: 5m
          labels:
            severity: warning
          annotations:
            summary: High error rate in YOUR_NAMESPACE
            description: More than 5 ERROR log lines per second over the last 5 minutes.
```

Refine the `expr` with LogQL — the same query language you use in Grafana's Explore view:

- `|= "ERROR"` — line contains `ERROR`
- `|~ "(ERROR|FATAL)"` — line matches a regex
- `| json | level="error"` — parse a JSON log line and match on the `level` field

If your application logs as JSON, the third form is the most precise. When the rule matches, the alert flows through your existing `AlertmanagerConfig` and lands in your Slack channel — the same channel that receives metric alerts.

## Next step

Continue to [Traces](../tracing/index.md) to follow requests across your services with distributed tracing.
