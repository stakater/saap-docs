# Overview

This section covers application development and deployment on {{ product_name }}. Content is organized into explanations, how-to guides, and tutorials for both the inner and outer development loops.

## User stories

Refer to the [User Stories](user-stories.md) to understand common developer journeys on {{ product_name }}.

## Explanation

- [Developer Training](./explanation/developer-training.md)

    Learn the fundamental concepts, languages, and technologies needed for application development on {{ product_name }}.

- [Inner vs Outer Loop](./explanation/inner-outer-loop.md)

    Understand the difference between the inner loop (local code iteration) and the outer loop (GitOps-based deployment).

- [Local Development Workflow](./explanation/local-development-workflow.md)

    Learn the local development workflow, including a diagram of the full cycle.

- [Plan your deployment](./explanation/plan-your-deployment.md)

    Learn how to evaluate your application's requirements, choose a deployment strategy, and plan your integration points before going to production.

- [Production best practices](./explanation/production-best-practices.md)

    Learn best practices for running applications in production, including high availability and security measures.

## How-to guides

- [Add Environment to Apps GitOps Repository](./how-to-guides/add-a-new-environment-to-apps-gitops/add-a-new-environment-to-application.md)

    Add a new environment to your application's GitOps workflow.

- [Build and Push your Image to Nexus](./how-to-guides/build-and-push-your-image/build-and-push-your-image.md)

    Build a container image and push it to Nexus so it is available for deployment.

- [Deploy Application with ArgoCD and Helm](./how-to-guides/deploy-app-with-argocd-and-helm/deploy-app-with-argocd-and-helm.md)

    Deploy your application using ArgoCD and Helm charts across multiple environments.

- [Enable metrics for Spring Boot Application](./how-to-guides/expose-spring-boot-metrics/expose-spring-boot-metrics.md)

    Expose metrics from your Spring Boot application and configure them for visualization.

- [Package and push your chart to Nexus](./how-to-guides/package-and-push-your-chart/package-and-push-your-chart.md)

    Package your application as a Helm chart and push it to a Nexus repository.

- [Application promotion](./how-to-guides/promote-your-application/promote-your-application.md)

    Promote your application across environments by versioning and sharing Helm charts with your team.

- [Backup and Restore a Stateful App using Velero](./how-to-guides/velero-stateful-app-example.md)

    Back up and restore a stateful app, its namespace, and PVCs using Velero.

- [Restore PVC data with GitOps](./how-to-guides/velero-restore-with-gitops.md)

    Back up and restore a GitOps-managed stateful app using Velero.

- [Deploy Multiple Applications with Tilt](./how-to-guides/deploy-multiple-apps-with-tilt/deploy-multiple-apps-with-tilt.md)

    Deploy multiple microservices in a sandbox environment using Tilt.

## Tutorials - inner loop

- [Nordmart Review 101](./tutorials/inner-loop/about-application/about-application.md)

    Explore the architecture, components, and dependencies of the Nordmart Review sample application.

- [Access your cluster](./tutorials/inner-loop/access-the-cluster/access-the-cluster.md)

    Learn how to access and interact with {{ product_name }}.

- [Enable alerts for your application](./tutorials/inner-loop/add-alerts/add-alerts.md)

    Configure alert notifications and triggers for your application to detect and respond to issues.

- [Configuring your application with Secrets and ConfigMaps](./tutorials/inner-loop/add-configmap/add-configmaps.md)

    Use ConfigMaps to externalize and manage your application's configuration.

- [Add Grafana Dashboard to your application](./tutorials/inner-loop/add-grafana-dashboard/add-grafana-dashboard.md)

    Create Grafana dashboards to visualize your application's performance metrics.

- [Add Network Policy to your application](./tutorials/inner-loop/add-network-policy/add-network-policy.md)

    Apply network policies to control pod-to-pod communication and isolate your application's traffic within {{ product_name }}.

- [Add Pod Disruption Budget (PDB) to your application](./tutorials/inner-loop/add-pdb/add-pdb.md)

    Add a Pod Disruption Budget to define availability constraints and prevent disruptions during updates or failures.

- [Adding External Secrets for your application](./tutorials/inner-loop/add-secret/add-secrets.md)

    Inject secrets from an external provider into your application.

- [Persist your application](./tutorials/inner-loop/add-storage/persist-app.md)

    Configure storage resources to persist data for your stateful application.

- [Configure Probes for your application](./tutorials/inner-loop/configure-probes/configure-probes.md)

    Configure readiness and liveness probes to ensure your application recovers automatically from failures.

- [Containerize the Application](./tutorials/inner-loop/containerize-app/containerize-app.md)

    Package your application and its dependencies into a container image.

- [Deploy your application](./tutorials/inner-loop/deploy-app/deploy-app.md)

    Deploy your application onto {{ product_name }} using Helm charts.

- [Expose your application](./tutorials/inner-loop/expose-app/expose-app.md)

    Expose your application to external traffic using services, load balancers, or Ingress controllers.

- [Monitor your application](./tutorials/inner-loop/monitor-your-app/monitor-your-app.md)

    Use {{ product_name }} monitoring tools to track your application's health and performance.

- [Package the Application](./tutorials/inner-loop/package-app/package-app.md)

    Package your application as a reusable Helm chart for deployment across environments.

- [Prepare the local environment](./tutorials/inner-loop/prepare-environment/prepare-env.md)

    Configure the local resources, settings, and dependencies needed to run your application.

- [Autoscaling your application](./tutorials/inner-loop/scale-app/scale-app.md)

    Configure horizontal scaling to handle varying workloads.

- [Tilt Zero to Hero](./tutorials/inner-loop/tilt-zero-to-hero/step-by-step-guide.md)

    Set up and configure Tilt to streamline your local development workflow.

- [Enable logging for your application](./tutorials/inner-loop/validate-logs/validate-logs.md)

    Validate your application's logging output to ensure events are tracked and troubleshooting is accurate.

- [Validate Auto Reload of your application](./tutorials/inner-loop/validate-auto-reload/validate-auto-reload.md)

    Integrate [Reloader](https://github.com/stakater/Reloader) into your application to automatically reload pods when configuration changes.

## Tutorials - outer loop

- [Access your cluster](./tutorials/outer-loop/access-cluster/access-the-cluster.md)

    Learn how to access, authenticate, and navigate your Kubernetes cluster.

- [Add Environment](./tutorials/outer-loop/add-build-environment/add-environment.md)

    Configure a dedicated build environment with the tools and resources needed to compile your application.

- [Add Pipeline to Your Application](./tutorials/outer-loop/add-ci-pipeline/01-overview.md)

    Set up a CI pipeline to automate testing, building, and deployment of your application.

- [Promote your application](./tutorials/outer-loop/promote-application/promote-app.md)

    Move your application through environments from development to production using pipelines and promotion procedures.
