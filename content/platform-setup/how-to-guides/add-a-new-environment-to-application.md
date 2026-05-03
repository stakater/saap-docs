# Add a new environment to an application

This guide explains how to add a new deployment environment to an existing application in your apps GitOps repository. You need this when you provision a new cluster or want to deploy an application to an additional environment such as `prod`.

This assumes the apps GitOps repository is already configured. If not, start with [Configure the apps GitOps repository](../tutorials/configure-apps-gitops-repo.md).

---

## Steps

1. Create an environment folder inside the application folder.

    In your apps GitOps repository, navigate to `<tenant>/<application>/` and create a folder named after the new environment. Using `gabbar` as the tenant and `stakater-nordmart-review` as the application:

    ```
    gabbar/
    └── stakater-nordmart-review/
        └── prod/
    ```

2. Add the Helm chart configuration for the new environment.

    Inside the `prod` folder, add `Chart.yaml` and `values.yaml` with configuration specific to this environment:

    ```
    gabbar/
    └── stakater-nordmart-review/
        └── prod/
            ├── Chart.yaml
            ├── values.yaml
            └── templates/
    ```

3. Create an ArgoCD Application in the tenant's `argocd-apps` folder pointing to this environment.

    Add a file at `gabbar/argocd-apps/prod/stakater-nordmart-review.yaml`:

    ```yaml
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      name: gabbar-prod-stakater-nordmart-review
      namespace: rh-openshift-gitops-instance
    spec:
      destination:
        namespace: gabbar-prod
        server: 'https://kubernetes.default.svc'
      project: gabbar
      source:
        path: gabbar/stakater-nordmart-review/prod
        repoURL: 'APPS_GITOPS_REPO_URL'
        targetRevision: HEAD
      syncPolicy:
        automated:
          prune: true
          selfHeal: true
    ```

4. Create a root-level ArgoCD Application pointing to the tenant's `argocd-apps/prod` folder.

    Add a file at `argocd-apps/<cluster>/gabbar-prod.yaml`. This tells ArgoCD to watch the tenant-level ArgoCD applications for this environment:

    ```yaml
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      name: gabbar-prod
      namespace: rh-openshift-gitops-instance
    spec:
      destination:
        namespace: rh-openshift-gitops-instance
        server: 'https://kubernetes.default.svc'
      project: gabbar
      source:
        path: gabbar/argocd-apps/prod
        repoURL: 'APPS_GITOPS_REPO_URL'
        targetRevision: HEAD
      syncPolicy:
        automated:
          prune: true
          selfHeal: true
    ```

5. Verify the infra GitOps repository has an ArgoCD Application watching `argocd-apps/<cluster>/`.

    If this is a new cluster, ensure the infra repository's `argocd-apps` folder includes an application pointing to this cluster's folder in the apps repository. See [Configure the apps GitOps repository](../tutorials/configure-apps-gitops-repo.md#link-the-apps-repository-to-the-infra-repository) for the linking step.

---

Commit and push your changes. ArgoCD will pick up the new application and deploy the environment within a few minutes.
