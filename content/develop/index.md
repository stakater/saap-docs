# Deploy

This section covers deploying applications to {{ product_name }} — from building your first container image to running ArgoCD-managed releases across multiple environments.

---

## How deployment works

{{ product_name }} uses an outer loop model: you build an image, package it as a Helm chart, push both to Harbor, then commit deployment configuration to your apps GitOps repository. ArgoCD detects the commit and deploys automatically — no manual `kubectl apply` required.

Read [Inner vs outer loop](explanation/inner-outer-loop.md) if you are new to this model, or [Plan your deployment](explanation/plan-your-deployment.md) to evaluate your application's requirements before you start.

---

## Quick start

Work through [Deploy a demo app](tutorials/deploy-demo-app.md) for a complete end-to-end walkthrough: build an image, push it to Harbor, package the chart, deploy via ArgoCD, and verify the result.

---

## Common tasks

| Scenario | Guide |
|---|---|
| Build a container image and push it to Harbor | [Build and push your image](how-to-guides/build-and-push-your-image/build-and-push-your-image.md) |
| Package a Helm chart and push it to Harbor | [Package and push your chart](how-to-guides/package-and-push-your-chart/package-and-push-your-chart.md) |
| Deploy an application using ArgoCD and Helm | [Deploy with ArgoCD and Helm](how-to-guides/deploy-app-with-argocd-and-helm/deploy-app-with-argocd-and-helm.md) |
| Expose an application on a custom hostname over https | [Expose your application](how-to-guides/expose-applications-to-internet/expose-applications-to-internet.md) |
| Rewrite URL paths at the ingress | [Path rewriting](how-to-guides/rewriting-path-annotation/path-rewriting.md) |
| Promote an application to the next environment | [Promote your application](how-to-guides/promote-your-application/promote-your-application.md) |

---

## Concepts

- [Inner vs outer loop](explanation/inner-outer-loop.md) — local iteration vs GitOps-based deployment
- [Plan your deployment](explanation/plan-your-deployment.md) — evaluate your application's requirements before you start
