# Downtime notifications

This guide shows you how to receive a notification when one of your monitored endpoints goes down.

## How it works

UptimeRobot probes the endpoints you registered with `EndpointMonitor`. When a probe fails, UptimeRobot fires an alert to the contacts attached to that monitor. Stakater manages both the IMC configuration and the UptimeRobot account — you provide the Slack webhook, Stakater registers it as the alert contact.

## 1. Create a Slack incoming webhook

Use a Slack bot account to manage incoming webhooks — an integration created under a personal account stops working if the user leaves.

1. In your Slack workspace, open **Administration → Manage Apps**.
1. Search the App Directory for **Incoming WebHooks** and click **Add to Slack**.
1. Pick the channel that should receive the alerts. A new channel can be created here.
1. Click **Add Incoming WebHooks Integration** and copy the generated **WebHook URL** from the next screen.
1. Optionally rename the webhook and add a custom icon so the alerts are easy to recognise.

## 2. Send the webhook to Stakater Support

Submit the WebHook URL to [Stakater Support](https://support.stakater.com/). Stakater registers it as an UptimeRobot alert contact and attaches it to the monitors created from your `EndpointMonitor` resources.

## 3. Enable EndpointMonitor for your application

Enable `endpointMonitor` in your application's `values.yaml` for the [Stakater Application Helm Chart](../helm-leader-chart/index.md):

```yaml
endpointMonitor:
  enabled: true
```

For the full set of supported fields, see [Add an EndpointMonitor](./add-monitors.md).

## 4. Validate the notification

Scale your application to zero replicas to simulate downtime:

```yaml
deployment:
  replicas: 0
```

Within a couple of minutes you should see a downtime alert in the Slack channel you configured. Restore the replica count once you have confirmed delivery.

## Next step

You have completed the Observe section. Continue to [Govern](../../govern/index.md) to see how the platform handles secrets, backups, and compliance.
