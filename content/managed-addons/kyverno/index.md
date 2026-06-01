# Kyverno

[Kyverno](https://github.com/kyverno/kyverno) is the Kubernetes-native policy engine that enforces security and compliance guardrails on every workload deployed to the platform.

## How it works

Stakater operates Kyverno on the cluster with a curated set of `ClusterPolicy` resources that block insecure configurations at admission time — before they reach the cluster. Policies cover container security context, image provenance, network policies, resource limits, and tenant scoping. You do not write or maintain these policies; Stakater curates and upgrades them centrally.

## What you do

Deploy applications normally through the [Stakater Application Helm Chart](../helm-leader-chart/index.md). If a resource you submit violates a policy, Kyverno rejects it at apply time and ArgoCD surfaces the error in the application's sync status. Read the error message, fix the offending field in `values.yaml`, and re-sync.

## Next step

Continue to [OpenBao](../vault/index.md) for secrets management.
