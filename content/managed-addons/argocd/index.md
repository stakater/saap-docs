# ArgoCD

ArgoCD is the GitOps continuous delivery engine that drives all deployments on the platform. When you push a change to your apps GitOps repository, ArgoCD detects the drift between Git and the cluster and syncs automatically — no manual deployment commands needed.

Access ArgoCD through Forecastle, your cluster's application dashboard. Use it to monitor application health, inspect sync status, and review deployment history.

---

## Deployment flow

Every application is represented as an ArgoCD Application pointing at your `apps-gitops-config` repository. To deploy a new version, update a chart version or image tag in that repository and push — ArgoCD handles the rest.

For a complete walkthrough, see [Deploy a new version via GitOps](../../develop/how-to-guides/deploy-app-with-argocd-and-helm/deploy-app-with-argocd-and-helm.md).
