# Environment Types

{{ product_name }} supports three kinds of environments for each tenant. Understanding the difference helps you plan where your work happens at each stage of development.

## Sandbox

Every developer in a tenant gets a personal sandbox namespace, provisioned automatically by Multi-Tenant Operator when they join. Sandbox namespaces are not managed through GitOps — they are scratch spaces for fast iteration and prototyping directly against the cluster. No monitoring or alerting is configured for sandbox namespaces.

## Preview

When a developer opens a pull request, Tronador automatically creates a short-lived preview environment for that PR. The environment is torn down when the PR is merged or closed. Preview environments let reviewers test real deployments before code reaches any permanent environment.

## Application environments

Persistent, GitOps-managed environments for your application — typically `dev`, `test`, `staging`, and `prod`. Each environment is a folder in your apps GitOps repository. Deployments are driven by ArgoCD syncing from Git.

Promotion between environments is a Git operation: open a pull request that bumps the chart version in `Chart.yaml` and the image tag in `values.yaml` for the target environment. ArgoCD applies the change once the PR is merged.

---

You now understand how environments are organized. The bootstrap steps ahead will create the repositories and configuration that make all of this work.

Continue to [Configure the infra GitOps repository](../tutorials/configure-infra-gitops-repo.md).
