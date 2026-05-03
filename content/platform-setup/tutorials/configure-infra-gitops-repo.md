# Configure the Infra GitOps Repository

By the end of this tutorial, you will have a working `infra-gitops-config` repository with your first tenant, quota, and ArgoCD application committed to it — and ArgoCD will be watching it.

This is the first of two bootstrap steps. The infra repository is where you define cluster-level resources: who can deploy, how much resource they get, and which cluster they can deploy to. The apps repository (next step) is where application workloads live.

**Prerequisites:**

- Your cluster has been provisioned by Stakater and ArgoCD is running.
- You have a personal access token (PAT) for your Git provider with read access to the repository you are about to create. This is stored in OpenBao under `git-pat-creds`.

A [template repository](https://github.com/NordMart/infra-gitops-config.git) is available to use as a starting point.

---

## Create the repository

1. Create an empty repository in your SCM (GitHub, GitLab, etc.) named `infra-gitops-config`.

2. Create an `ExternalSecret` on the cluster that gives ArgoCD read access to the repository. Replace `INFRA_GITOPS_REPO_URL` with your actual repository URL.

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: infra-gitops-creds
  namespace: rh-openshift-gitops-instance
spec:
  refreshInterval: 1m
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
    name: infra-gitops-creds
    template:
      metadata:
        labels:
          argocd.argoproj.io/secret-type: repository
      data:
        name: infra-gitops-creds
        password: '{% raw %}{{ .password | toString }}{% endraw %}'
        username: '{% raw %}{{ .username | toString }}{% endraw %}'
        project: root-tenant
        type: git
        url: 'INFRA_GITOPS_REPO_URL'
```

---

## Define the folder structure

The repository is organized by cluster. Create the following structure for your cluster (replace `CLUSTER_NAME` with your cluster's name):

3. Create a folder at the root named after your cluster, e.g. `dev`.

4. Inside it, create two folders: `argocd-apps` and `tenant-operator-config`.

5. Inside `tenant-operator-config`, create two folders: `tenants` and `quotas`.

Your structure should now look like this:

```
infra-gitops-config/
└── dev/
    ├── argocd-apps/
    └── tenant-operator-config/
        ├── tenants/
        └── quotas/
```

---

## Add your first tenant

6. Create a `Tenant` resource in the `tenants` folder. This defines the team, their allowed repositories, and the namespaces they get. Replace the owners, repository URLs, and namespace names with your own values.

    ```yaml
    apiVersion: tenantoperator.stakater.com/v1beta1
    kind: Tenant
    metadata:
      name: arsenal
    spec:
      quota: arsenal-large
      owners:
        users:
        - your-user@example.com
      argocd:
          sourceRepos:
          - 'https://github.com/your-organization/infra-gitops-config'
          - 'https://github.com/your-organization/apps-gitops-config'
          - '<YOUR-HARBOR-REGISTRY-URL>'
      templateInstances:
      - spec:
          template: tenant-vault-access
          sync: true
      namespaces:
      - dev
      - staging
      - prod
    ```

    !!! note
        Replace `<YOUR-HARBOR-REGISTRY-URL>` with the URL from your Harbor registry. Find it via Forecastle.

7. Create a matching `Quota` resource in the `quotas` folder. The quota name must match the value in `spec.quota` of the Tenant above.

    ```yaml
    apiVersion: tenantoperator.stakater.com/v1beta1
    kind: Quota
    metadata:
      name: arsenal-large
      annotations:
        quota.tenantoperator.stakater.com/is-default: "false"
    spec:
      resourcequota:
        hard:
          requests.cpu: "16"
          requests.memory: 32Gi
      limitrange:
        limits:
          - defaultRequest:
              cpu: 10m
              memory: 50Mi
            type: Container
    ```

---

## Create the ArgoCD application

8. Create an ArgoCD `Application` in the `argocd-apps` folder. This tells ArgoCD to watch the `tenant-operator-config` folder and apply everything in it.

    ```yaml
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      name: CLUSTER_NAME-tenant-operator-config
      namespace: rh-openshift-gitops-instance
    spec:
      destination:
        namespace: rh-openshift-gitops-instance
        server: 'https://kubernetes.default.svc'
      source:
        path: CLUSTER_NAME/tenant-operator-config
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

    Replace `CLUSTER_NAME` with your cluster's folder name and `INFRA_GITOPS_REPO_URL` with your repository URL.

---

## Bootstrap ArgoCD

9. Apply the root ArgoCD application to the cluster. This is the single application ArgoCD uses as its entry point into the entire infra repository.

    ```yaml
    apiVersion: argoproj.io/v1alpha1
    kind: Application
    metadata:
      name: infra-gitops-config
      namespace: rh-openshift-gitops-instance
    spec:
      destination:
        namespace: rh-openshift-gitops-instance
        server: 'https://kubernetes.default.svc'
      project: default
      source:
        path: CLUSTER_NAME/argocd-apps
        repoURL: 'INFRA_GITOPS_REPO_URL'
        targetRevision: HEAD
      syncPolicy:
        automated:
          prune: true
          selfHeal: true
    ```

10. Log in to ArgoCD and verify that the `infra-gitops-config` application is present and that its child application `tenant-operator-config` has synced successfully.

---

Your infra repository is now bootstrapped. ArgoCD is watching it and your first tenant is live on the cluster.

For more on the `Tenant` and `Quota` resources, see [Multi Tenant Operator custom resources](https://docs.stakater.com/mto/main/customresources.html).

Continue to [Configure the apps GitOps repository](configure-apps-gitops-repo.md).
