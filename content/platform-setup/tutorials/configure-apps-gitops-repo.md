# Configure the Apps GitOps Repository

By the end of this tutorial, your `apps-gitops-config` repository will be structured, linked to the infra repository, and ArgoCD will be watching it. Application deployments for your first tenant will be driven from Git.

This is the second bootstrap step. If you haven't yet completed [Configure the infra GitOps repository](configure-infra-gitops-repo.md), do that first.

**Prerequisites:**

- The infra GitOps repository is set up and ArgoCD has synced it.
- You have a personal access token (PAT) for this new repository stored in OpenBao under `git-pat-creds`.

A [template repository](https://github.com/stakater-lab/apps-gitops-config.git) is available to use as a starting point.

---

## Create the repository

1. Create an empty repository in your SCM named `apps-gitops-config`.

---

## Build the folder structure

The apps repository is organized as: **tenant → application → environment**. Each level is a folder.

2. Create a folder at the root named after your tenant (e.g. `arsenal` — the same tenant you defined in the infra repository).

3. Inside the tenant folder, create an `argocd-apps` folder. This is where ArgoCD Application resources for this tenant will live.

4. Create an application folder inside the tenant folder (e.g. `stakater-nordmart-review`).

5. Inside the application folder, create a folder for each environment (e.g. `dev` and `staging`). These folders will hold the Helm chart or plain YAML for each environment.

Your structure should now look like this:

```
apps-gitops-config/
└── arsenal/
    ├── argocd-apps/
    │   ├── dev/
    │   └── staging/
    └── stakater-nordmart-review/
        ├── dev/
        └── staging/
```

---

## Create ArgoCD applications for each environment

For each environment, create an ArgoCD Application resource in the matching `argocd-apps/<env>/` folder. The application points to the deployment manifests in the sibling application folder.

6. Create `arsenal/argocd-apps/dev/stakater-nordmart-review.yaml`:

    ```yaml
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      name: arsenal-dev-stakater-nordmart-review
      namespace: rh-openshift-gitops-instance
    spec:
      destination:
        namespace: arsenal-dev
        server: 'https://kubernetes.default.svc'
      project: arsenal
      source:
        path: arsenal/stakater-nordmart-review/dev
        repoURL: 'APPS_GITOPS_REPO_URL'
        targetRevision: HEAD
      syncPolicy:
        automated:
          prune: true
          selfHeal: true
    ```

7. Create a matching file for the `staging` environment in `arsenal/argocd-apps/staging/`.

---

## Create the root ArgoCD applications

The root-level `argocd-apps` folder is the entry point per cluster. It contains one ArgoCD Application per tenant-environment combination, pointing to the tenant-level `argocd-apps` above.

8. Create `argocd-apps/<cluster>/` folders for each cluster you are deploying to (e.g. `argocd-apps/dev-cluster/`).

9. Create an ArgoCD Application in `argocd-apps/dev-cluster/arsenal-dev.yaml` pointing to the tenant-level argocd-apps for dev:

    ```yaml
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      name: arsenal-dev
      namespace: rh-openshift-gitops-instance
    spec:
      destination:
        namespace: rh-openshift-gitops-instance
        server: 'https://kubernetes.default.svc'
      project: arsenal
      source:
        path: arsenal/argocd-apps/dev
        repoURL: 'APPS_GITOPS_REPO_URL'
        targetRevision: HEAD
      syncPolicy:
        automated:
          prune: true
          selfHeal: true
    ```

---

## Link the apps repository to the infra repository

Now you add the apps repository as a watched source inside the infra repository. This is what closes the loop — ArgoCD, bootstrapped from the infra repo, will start watching the apps repo.

In your **infra** repository, inside the cluster folder (e.g. `dev/`):

10. Create a `gitops-repositories/` folder and add an `ExternalSecret` that gives ArgoCD read access to the apps repository:

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: apps-gitops-creds
  namespace: rh-openshift-gitops-instance
spec:
  refreshInterval: 1m0s
  secretStoreRef:
    name: tenant-vault-shared-secret-store
    kind: SecretStore
  data:
  - remoteRef:
      key: git-pat-creds
      property: username
    secretKey: username
  - remoteRef:
      key: git-pat-creds
      property: password
    secretKey: password
  target:
    name: apps-gitops-creds
    template:
      metadata:
        labels:
          argocd.argoproj.io/secret-type: repository
      data:
        name: apps-gitops-creds
        password: "{% raw %}{{ .password | toString }}{% endraw %}"
        username: "{% raw %}{{ .username | toString }}{% endraw %}"
        project: arsenal
        type: git
        url: "https://github.com/YOUR_ORG/apps-gitops-config.git"
```

11. Add an ArgoCD Application in `dev/argocd-apps/gitops-repositories.yaml` that deploys the secret above:

    ```yaml
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      name: gitops-repositories
      namespace: rh-openshift-gitops-instance
    spec:
      destination:
        server: 'https://kubernetes.default.svc'
      source:
        path: dev/gitops-repositories
        repoURL: 'INFRA_GITOPS_REPO_URL'
        targetRevision: HEAD
        directory:
          recurse: true
      project: root-tenant
      syncPolicy:
        automated:
          prune: true
          selfHeal: true
    ```

12. Add an ArgoCD Application in `dev/argocd-apps/apps-gitops-config.yaml` that watches the root argocd-apps in the apps repository:

    ```yaml
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      name: apps-gitops-config
      namespace: rh-openshift-gitops-instance
    spec:
      destination:
        namespace: rh-openshift-gitops-instance
        server: 'https://kubernetes.default.svc'
      project: root-tenant
      source:
        path: argocd-apps/dev-cluster
        repoURL: 'APPS_GITOPS_REPO_URL'
        targetRevision: HEAD
      syncPolicy:
        automated:
          prune: true
          selfHeal: true
    ```

---

## Verify

13. Log in to ArgoCD and open the `infra-gitops-config` application. Verify that `gitops-repositories` and `apps-gitops-config` have appeared as child applications and synced successfully.

The image below shows a fully linked infra-apps structure in ArgoCD:

![ArgoCD apps-of-apps structure](../images/ArgoCD-Infra-repo-App.png)

---

Both repositories are now set up and ArgoCD is managing your full GitOps structure. Any commit to the apps repository will be picked up and applied to the cluster automatically.

The next step is connecting your identity provider so your team can log in.

Continue to [Connect your identity provider](../how-to-guides/keycloak-idp.md).
