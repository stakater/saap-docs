# Configure the Infra GitOps Repository

By the end of this tutorial, you will have a working `infra-gitops-config` repository with your first tenant, quota, and ArgoCD application committed to it — and ArgoCD will be watching it.

This is the first of two bootstrap steps. The infra repository is where you define cluster-level resources: who can deploy, how much resource they get, and which cluster they can deploy to. The apps repository (next step) is where application workloads live.

**Prerequisites:**

- Your cluster has been provisioned by Stakater and ArgoCD is running.

A [template repository](https://github.com/NordMart/infra-gitops-config.git) is available to use as a starting point.

---

## 1. Create a personal access token

ArgoCD needs read access to your repository. Create a personal access token (PAT) on your Git provider before you create the repository.

### GitHub: Fine-grained PAT (recommended)

[Create a fine-grained token](https://github.blog/2022-10-18-introducing-fine-grained-personal-access-tokens-for-github/) scoped to your GitOps repositories. Required permissions:

| Permission | Level |
|---|---|
| Actions | Read and write |
| Administration | Read and write |
| Commit statuses | Read only |
| Contents | Read and write |
| Deployments | Read only |
| Metadata | Read only |
| Pull requests | Read and write |

Note: Fine-grained PATs cannot be edited after creation. Create the repositories first if you want to scope the token to specific repos, or create the token with organization-wide scope and tighten it later.

### GitHub: Classic PAT

[Create a classic personal access token](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) with `repo` permissions. This grants access to all repositories in your account.

### SSH key (alternative)

[Generate an SSH key pair](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key) and add the public key to your [GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) or as a [deploy key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#deploy-keys) on the specific repository.

---

## 2. Store the token in OpenBao

Store your PAT in OpenBao at the path `git-pat-creds` with two fields:

- `username` — your Git provider username
- `password` — the PAT you just created

ArgoCD retrieves these credentials at sync time via ExternalSecrets. The same secret is reused in the apps repository setup in the next tutorial.

---

## 3. Create the repository

Create an empty repository in your SCM (GitHub, GitLab, etc.) named `infra-gitops-config`.

Then create an `ExternalSecret` on the cluster that gives ArgoCD read access to the repository. Replace `INFRA_GITOPS_REPO_URL` with your actual repository URL.

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

## 4. Define the folder structure

The repository is organized by cluster. Create the following structure (replace `dev` with your cluster name):

```text
infra-gitops-config/
└── dev/
    ├── argocd-apps/
    └── tenant-operator-config/
        ├── tenants/
        └── quotas/
```

---

## 5. Add your first tenant

Create a `Tenant` resource in the `tenants` folder. Replace the owners, repository URLs, and namespace names with your own values.

```yaml
apiVersion: tenantoperator.stakater.com/v1beta1
kind: Tenant
metadata:
  name: TENANT_NAME
spec:
  quota: TENANT_NAME-large
  owners:
    users:
    - your-user@example.com
  argocd:
      sourceRepos:
      - 'https://github.com/your-organization/infra-gitops-config'
      - 'https://github.com/your-organization/apps-gitops-config'
      - 'YOUR_HARBOR_REGISTRY_URL'
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
    Replace `YOUR_HARBOR_REGISTRY_URL` with the URL from your Harbor registry. Find it via Forecastle.

Create a matching `Quota` resource in the `quotas` folder. The quota name must match the value in `spec.quota` above.

```yaml
apiVersion: tenantoperator.stakater.com/v1beta1
kind: Quota
metadata:
  name: TENANT_NAME-large
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

## 6. Create the ArgoCD application

Create an ArgoCD `Application` in the `argocd-apps` folder. This tells ArgoCD to watch the `tenant-operator-config` folder and apply everything in it.

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

## 7. Bootstrap ArgoCD

Apply the root ArgoCD application to the cluster. This is the single application ArgoCD uses as its entry point into the entire infra repository.

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

---

## 8. Verify

Log in to ArgoCD and confirm that the `infra-gitops-config` application is present and that its child application `tenant-operator-config` has synced successfully.

In the ArgoCD UI, click **Settings > Repositories** to verify the `infra-gitops-config` repository shows a green connected status.

If the status shows **Failed**, hover over the error icon to see the message.

### SSH handshake failed: key mismatch

Check the `argocd-ssh-known-hosts-cm` ConfigMap in the ArgoCD namespace. The public key for your repository host must be present in `ssh_known_hosts`. See [known host public keys](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/#ssh-known-host-public-keys) for the full list. If the error persists, contact [Stakater Support](https://support.stakater.com).

---

Your infra repository is now bootstrapped. ArgoCD is watching it and your first tenant is live on the cluster.

For more on the `Tenant` and `Quota` resources, see [Multi Tenant Operator custom resources](https://docs.stakater.com/mto/main/customresources.html).

Continue to [Configure the apps GitOps repository](configure-apps-gitops-repo.md).
