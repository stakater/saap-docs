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
1. [Connect your identity provider](how-to-guides/keycloak-idp.md) — federate your existing IDP into your Keycloak realm
1. [Configure user access](how-to-guides/user-access.md) — assign roles to your teams

---

## Identity & Access

Connect your organization's identity provider and control who can access what:

- [Connect Keycloak as an identity provider](how-to-guides/keycloak-idp.md)
- [Connect Google](how-to-guides/google-idp.md)
- [Connect Azure AD](how-to-guides/azure-idp.md)
- [Configure Azure group sync](how-to-guides/azure-gso.md)
- [Configure SAML](how-to-guides/saml-idp.md)
- [Configure authorization roles](how-to-guides/authorization-roles.md)
- [Configure user access](how-to-guides/user-access.md)

---

## Networking

Configure custom domains and automate TLS certificate management:

- [Configure custom domains](how-to-guides/custom-domains.md)
- [Configure TLS certificates](how-to-guides/tls-certs.md)
- [Use HTTP-01 certificate challenges](how-to-guides/http01-certs.md)

---

## Day-2 Operations

Recurring tasks for managing your platform after bootstrap:

- [Add a new environment to an application](how-to-guides/add-a-new-environment-to-application.md)

---

Once your platform is set up, head to **[Deploy](../develop/tutorials/deploy-demo-app.md)** to deploy your first application.
