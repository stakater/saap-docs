# Frequently Asked Questions

## 1. What is GitOps?

_GitOps is a way to do operations, by using Git as a single source of truth, and updating the state of the operating configuration automatically, based on a Git repository_.

## 2. How does GitOps differ from Infrastructure as Code?

_GitOps builds on top of Infrastructure as Code, providing application level concerns, as well as an operations model_.

## 3. Can I use a CI server to orchestrate convergence in the cluster?

_You could apply updates to the cluster from the CI server, but it won't continuously deploy the changes to the cluster, which means that drift won't be detected and corrected._

## 4. Should I abandon my CI tool?

_No, you'll want  CI to validate the changes that GitOps is applying._

## 5. Why choose Git and not a Configuration Database instead? / Why is git the source of truth?

_Git has strong auditability, and it fits naturally into a developer's flow._

## 6. How do you keep my tokens secret in the Git repository?

_Secrets are stored in OpenBao and synced into your workloads via the External Secrets Operator. They are never stored as plain text in Git._

## 7. How do I get started?

_Add some resources to a directory, and git commit and push, then ask ArgoCD to deploy the repository, change your resource, git commit and push, and the change should be deployed automatically._

## 8. How does CI integrate with GitOps?

_Your CI pipeline builds and pushes the container image, then updates the image tag in Git. ArgoCD detects the change and deploys it to the cluster automatically._

## 9. How is GitOps different from DevOps?

_GitOps is a subset of DevOps, specifically focussed on deploying the application (and infrastructure) through a Git flow-like process._

## 10. How could small teams benefit from GitOps?

_GitOps is about speeding up application feedback loops, with more automation, it frees up developers to work on the product features that customers love._
