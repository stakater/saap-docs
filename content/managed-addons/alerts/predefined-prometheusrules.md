# Predefined PrometheusRules

This page lists the PrometheusRules that {{ product_name }} ships out of the box. You can route their alerts to your channels — there is no need to write the rules yourself.

## How it works

The rules below are deployed and evaluated by the platform's Mimir ruler against every workload on the cluster. When one fires, the alert is routed through the same Alertmanager that handles your custom alerts — your `AlertmanagerConfig` (see [Configure application alerting](./workload-application-alerts.md)) picks them up automatically based on namespace.

## What you get

### Kubernetes apps

| Name                              | Description |
|-----------------------------------|-------------|
| KubePodCrashLooping               | Pod `Namespace/Pod` is restarting N times / 5 minutes. |
| KubePodNotReady                   | Pod `Namespace/Pod` has been in a non-ready state for longer than 15 minutes |
| KubeDeploymentGenerationMismatch  | Deployment generation for `Namespace/Deployment` does not match, this indicates that the Deployment has failed but has not been rolled back. |
| KubeDeploymentReplicasMismatch    | Deployment `Namespace/Deployment` has not matched the expected number of replicas for longer than 15 minutes. |
| KubeStatefulSetReplicasMismatch   | StatefulSet `Namespace/StatefulSet` has not matched the expected number of replicas for longer than 15 minutes |
| KubeStatefulSetGenerationMismatch | StatefulSet generation for `Namespace/StatefulSet` does not match, this indicates that the StatefulSet has failed but has not been rolled back. |
| KubeStatefulSetUpdateNotRolledOut | StatefulSet `Namespace/StatefulSet` update has not been rolled out. |
| KubeDaemonsetRolloutStuck         | Daemonset `Namespace/Daemonset` has not finished or progressed for at least 15 minutes. |
| KubeContainerWaiting              | Pod `Namespace/Pod` container `Container` has been in waiting state for longer than 1 hour. |
| KubeDaemonsetNotScheduled         | Pods of Daemonset `Namespace/Daemonset` are not scheduled. |
| KubeJobCompletion                 | Job `Namespace/Job` is taking more than 12 hours to complete. |
| KubeJobFailed                     | Job `Namespace/Job` failed to complete. Removing failed job after investigation should clear this alert. |
| KubeHpaReplicasMismatch           | HPA (Horizontal Pod Autoscaler) `Namespace/HPA` has not matched the desired number of replicas for longer than 15 minutes. |
| KubeHpaMaxedOut                   | HPA (Horizontal Pod Autoscaler) `Namespace/HPA` has been running at max replicas for longer than 15 minutes. |

### Kubernetes storage

| Name                              | Description |
|-----------------------------------|-------------|
| KubePersistentVolumeFillingUp     | The PersistentVolume claimed by `PersistentVolume` in Namespace `Namespace` is only `Percentage %` free. |
| KubePersistentVolumeErrors        | The persistent volume `PersistentVolume` has status `Failed/Pending`. |

## Next step

Continue to [Log alerts](./log-alerts.md) to alert on log content as well as metrics.
