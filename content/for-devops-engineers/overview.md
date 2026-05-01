# Overview

This section covers everything you need as a DevOps Engineer to set up GitOps-based CI/CD workflows. You are expected to have elevated permissions in your SCM provider to create tokens and SSH keys.

GitOps is managed through two repositories with distinct purposes:

- **`Apps GitOps Config`**: Used for delivering applications belonging to tenants.
- **`Infra GitOps Config`**: Used for delivering cluster-scoped resources for application tenants or other services.

You can pick any name for these two repositories as long as it reflects its purpose.

## Explanation

- [GitOps for application delivery](./explanation/gitops-intro.md): Learn the GitOps methodology in the context of application delivery and how it differs from DevOps.

- [Stakater opinionated GitOps structure](./explanation/gitops-structure.md): Understand how Stakater recommends organizing GitOps repositories, directory structures, and naming conventions for managing infrastructure and application configurations.

- [Types of environments](./explanation/types-of-environments.md): Explore the different environments involved in Stakater's application delivery.

- [Stakater Tekton Chart](./explanation/stakater-tekton-chart.md): Learn about the Helm chart that streamlines configurations and components for Tekton pipelines to build efficient CI/CD.

- [Frequently asked questions](./explanation/faq.md): Find answers to common questions about GitOps-based application delivery.

## How-to guides

- [Add cluster task](./how-to-guides/add-a-cluster-task/add-cluster-task.md): Add a cluster task to the Tekton pipeline.

- [Configure repository secret for ArgoCD](./how-to-guides/configure-repository-secret/configure-repository-secret.md): Configure repository secrets for Infra and Apps GitOps repositories.

- [Use a cluster task in pipeline](./how-to-guides/use-a-cluster-task-in-pipeline/use-a-clustertask-in-pipeline.md): Add a cluster task to your pipeline.

## Tutorials

- [Configure Infra GitOps repository](./tutorials/01-configure-infra-gitops-config/configure-infra-gitops-repo.md): Set up the infrastructure GitOps repository, align its directory and file structure, and add tenant and ArgoCD applications.

- [Configure Apps GitOps repository](./tutorials/02-configure-apps-gitops-config/configure-apps-gitops-repo.md): Set up the application GitOps repository, align its directory and file structure, add deployment manifests, and link it to the Infra GitOps repository.

- [Deploy demo app](./tutorials/03-deploy-demo-app/deploy-demo-app.md): Deploy a demo application using Stakater's GitOps techniques, including building and pushing the application image, creating an application chart, and pushing it to the Helm repository.
