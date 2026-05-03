# Platform Setup

{{ product_name }} uses two GitOps repositories as the source of truth for your entire platform — one for cluster-level infrastructure (tenants, quotas, namespaces) and one for application workloads (deployments, environments). Setting these up is the first thing you do after your cluster is provisioned.

This section covers the one-time bootstrap sequence and the ongoing self-service tasks for managing access, networking, and teams.

---

## Concepts

Read these before you start if you are new to the GitOps model {{ product_name }} uses:

- [How GitOps works](explanation/gitops-intro.md) — why Git is the source of truth and how changes flow to your cluster
- [GitOps repository structure](explanation/gitops-structure.md) — the two-repository layout and how the infra and apps repos relate
- [Environment types](explanation/types-of-environments.md) — sandbox namespaces, preview environments, and application environments

---

## Bootstrap

Run these steps once, in order, when your cluster is first provisioned:

1. [Configure the infra GitOps repository](tutorials/configure-infra-gitops-repo.md) — define tenants, quotas, and cluster-level resources
1. [Configure the apps GitOps repository](tutorials/configure-apps-gitops-repo.md) — register your applications and environments for GitOps delivery
1. [Connect your identity provider](how-to-guides/keycloak-idp.md) — federate your existing IdP into your Keycloak realm
1. [Configure user access](how-to-guides/user-access.md) — assign roles to your teams

---

## Identity & Access

### Identity providers

Federate your organization's existing accounts so users can log in without a separate password:

| Provider | Guides |
|---|---|
| Keycloak | [Connect Keycloak](how-to-guides/keycloak-idp.md) |
| Google | [Connect Google](how-to-guides/google-idp.md) |
| Azure AD | [Azure AD overview](how-to-guides/azure-ad/index.md) — connect + group sync |
| SAML | [Connect SAML](how-to-guides/saml-idp.md) |

### Access control

Define what authenticated users are allowed to do:

- [Configure authorization roles](how-to-guides/authorization-roles.md)
- [Configure user access](how-to-guides/user-access.md)

---

## Networking

By default, applications are reachable on the cluster's built-in domain. Configure networking when you need your own domain name, HTTPS certificates, or automated DNS management.

| Scenario | Guide |
|---|---|
| Serve an application on your own domain | [Configure custom domains](how-to-guides/custom-domains.md) |
| Add TLS to a public single hostname (no DNS credentials needed) | [Use http-01 certificate challenges](how-to-guides/http01-certs.md) |
| Wildcard certificate or cluster without public internet access | [Configure TLS certificates](how-to-guides/tls-certs.md) |

- [Configure custom domains](how-to-guides/custom-domains.md)
- [Configure TLS certificates](how-to-guides/tls-certs.md)
- [Use http-01 certificate challenges](how-to-guides/http01-certs.md)

---

## Day-2 Operations

Recurring tasks for managing your platform after bootstrap:

- [Add a new tenant](how-to-guides/add-a-new-tenant.md)
- [Add a new application](how-to-guides/add-a-new-application.md)
- [Add a new environment](how-to-guides/add-a-new-environment-to-application.md)

---

Once your platform is set up, head to **[Deploy](../develop/tutorials/deploy-demo-app.md)** to deploy your first application.
