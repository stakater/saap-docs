# Develop

This section covers building, deploying, and running applications on {{ product_name }}.

## Explanation

- [Developer Training](./explanation/developer-training.md) — fundamental concepts and technologies for development on {{ product_name }}
- [Inner vs Outer Loop](./explanation/inner-outer-loop.md) — local iteration vs GitOps-based deployment
- [Local Development Workflow](./explanation/local-development-workflow.md) — full local development cycle with Tilt
- [Plan your deployment](./explanation/plan-your-deployment.md) — evaluate requirements and choose a deployment strategy
- [Production best practices](./explanation/production-best-practices.md) — high availability and security for production workloads

## Tutorials

- [Deploy a demo app](./tutorials/deploy-demo-app.md) — end-to-end walkthrough: build an image, push to Harbor, deploy via ArgoCD

### Inner loop (local development)

- [Prepare the local environment](./tutorials/inner-loop/prepare-environment/prepare-env.md)
- [About the sample application](./tutorials/inner-loop/about-application/about-application.md)
- [Access your cluster](./tutorials/inner-loop/access-the-cluster/access-the-cluster.md)
- [Containerize the application](./tutorials/inner-loop/containerize-app/containerize-app.md)
- [Package the application](./tutorials/inner-loop/package-app/package-app.md)
- [Deploy your application](./tutorials/inner-loop/deploy-app/deploy-app.md)
- [Add secrets](./tutorials/inner-loop/add-secret/add-secrets.md)
- [Add ConfigMaps](./tutorials/inner-loop/add-configmap/add-configmaps.md)
- [Configure probes](./tutorials/inner-loop/configure-probes/configure-probes.md)
- [Persist your application](./tutorials/inner-loop/add-storage/persist-app.md)
- [Expose your application](./tutorials/inner-loop/expose-app/expose-app.md)
- [View logs](./tutorials/inner-loop/validate-logs/validate-logs.md)
- [Monitor your application](./tutorials/inner-loop/monitor-your-app/monitor-your-app.md)
- [Expose metrics](./tutorials/inner-loop/expose-metrics/expose-metrics.md)
- [Add alerts](./tutorials/inner-loop/add-alerts/add-alerts.md)
- [Add a Grafana dashboard](./tutorials/inner-loop/add-grafana-dashboard/add-grafana-dashboard.md)
- [Autoscale your application](./tutorials/inner-loop/scale-app/scale-app.md)
- [Backup and restore](./tutorials/inner-loop/add-backup-schedule/backup-restore.md)
- [Tilt zero to hero](./tutorials/inner-loop/tilt-zero-to-hero/step-by-step-guide.md)

### Outer loop (GitOps delivery)

- [Access your cluster](./tutorials/outer-loop/access-cluster/access-the-cluster.md)
- [Promote your application](./tutorials/outer-loop/promote-application/promote-app.md)

## How-to guides

- [Build and push your image to Harbor](./how-to-guides/build-and-push-your-image/build-and-push-your-image.md)
- [Package and push your chart to Harbor](./how-to-guides/package-and-push-your-chart/package-and-push-your-chart.md)
- [Deploy application with ArgoCD and Helm](./how-to-guides/deploy-app-with-argocd-and-helm/deploy-app-with-argocd-and-helm.md)
- [Promote your application](./how-to-guides/promote-your-application/promote-your-application.md)
- [Deploy multiple apps with Tilt](./how-to-guides/deploy-multiple-apps-with-tilt/deploy-multiple-apps-with-tilt.md)
- [Expose your application](./how-to-guides/expose-applications-to-internet/expose-applications-to-internet.md)
- [Enable Spring Boot metrics](./how-to-guides/expose-spring-boot-metrics/expose-spring-boot-metrics.md)
- [Remote debugging (.NET)](./how-to-guides/remote-debugging/remote-debugging-dotnet.md)
- [Remote debugging with mirrord](./how-to-guides/remote-debugging-mirrord/remote-debugging-mirrord-tilt.md)
- [Path rewriting](./how-to-guides/rewriting-path-annotation/path-rewriting.md)
