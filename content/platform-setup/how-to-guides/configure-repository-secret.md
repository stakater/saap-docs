# Configure a repository secret for ArgoCD

ArgoCD needs credentials to pull from private repositories. This page explains how to create a GitHub personal access token (PAT) or SSH key, store it securely, and connect it to ArgoCD.

---

## 1. Create credentials in GitHub

Choose one of the following:

### PAT (Classic)

[Create a personal access token](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) with `repo` permissions. A classic PAT grants access to all repositories in your account.

### PAT (Fine-grained)

[Create a fine-grained token](https://github.blog/2022-10-18-introducing-fine-grained-personal-access-tokens-for-github/) scoped to specific repositories. This is the recommended option because it limits access to only the GitOps repositories.

Required permissions for your GitOps repositories:

| Permission | Level |
|---|---|
| Actions | Read and write |
| Administration | Read and write |
| Commit statuses | Read only |
| Contents | Read and write |
| Deployments | Read only |
| Metadata | Read only |
| Pull requests | Read and write |

Note: Fine-grained PATs cannot be edited after creation. Create the repositories first, then add them to the PAT.

### SSH key

[Generate an SSH key pair](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key) and add the public key to your [GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) (works for multiple repos) or as a [deploy key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#deploy-keys) on a single repository.

---

## 2. Store credentials in OpenBao

Store your PAT or SSH key in OpenBao so that ArgoCD can retrieve it via ExternalSecrets. The infra GitOps bootstrap stores credentials under `git-pat-creds` — use the same path for additional repositories or follow the same pattern.

See [Configure the infra GitOps repository](../tutorials/configure-infra-gitops-repo.md) for the ExternalSecret template.

---

## 3. Create a Kubernetes Secret in the ArgoCD namespace

As an alternative to ExternalSecrets, you can create a Secret directly. Each repository secret must include the repository URL and credentials.

**For HTTPS:**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: private-repo
  namespace: rh-openshift-gitops-instance
  labels:
    argocd.argoproj.io/secret-type: repository
stringData:
  type: git
  url: https://github.com/your-org/your-repo
  username: my-username
  password: my-pat
```

**For SSH:**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: private-repo
  namespace: rh-openshift-gitops-instance
  labels:
    argocd.argoproj.io/secret-type: repository
stringData:
  type: git
  url: git@github.com:your-org/your-repo
  sshPrivateKey: |
    -----BEGIN OPENSSH PRIVATE KEY-----
    ...
    -----END OPENSSH PRIVATE KEY-----
```

See [ArgoCD declarative setup](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/#repositories) for the full reference.

---

## 4. Verify the connection

Log in to the ArgoCD UI, click **Settings** in the left sidebar, then **Repositories**. The repository should show a green connected status.

![ArgoCD repositories](../images/ArgoCD-repositories.png)

---

## Troubleshooting

### Connection failed

Hover over the error icon next to **Failed** to see the error message.

### SSH handshake failed: key mismatch

Check the `argocd-ssh-known-hosts-cm` ConfigMap in the ArgoCD namespace. The public key for your repository host must be present in `ssh_known_hosts`. See [known host public keys](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/#ssh-known-host-public-keys) for the full list.

If the error persists, contact [Stakater Support](https://support.stakater.com).

---

With your repository connected, continue to [Add a new environment to an application](add-a-new-environment-to-application.md).
