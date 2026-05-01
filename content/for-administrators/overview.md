# Overview

This section covers the administration of {{ product_name }} on OpenShift. It is intended for cluster administrators who need to plan, secure, and maintain their environment.

## User stories

Read the [User Stories](user-stories.md) to understand common administrator journeys with {{ product_name }}.

## Explanation

- [Privileged roles available in {{ product_name }}](./secure-your-cluster/authorization-roles.md)

    Learn what privileged roles exist in {{ product_name }} and what access each role grants.

- [Number of clusters](./explanation/number-of-clusters.md)

    Understand how to decide how many clusters your organization needs.

## How-to guides

### Plan your environment

- [Size your environment](./plan-your-environment/sizing.md)

    Assess your workload requirements and choose the right node sizes and counts for your cluster.

### Secure your cluster

- [Configure user access](./secure-your-cluster/user-access.md)

    Set up identity providers to control who can authenticate to your cluster.

- [Whitelist IPs on routes](./secure-your-cluster/secure-routes.md)

    Restrict access to specific OpenShift routes by allowing only defined IP addresses.

- [Configure Google identity provider](./secure-your-cluster/google-idp.md)

    Integrate Google as an identity provider so users can sign in with their Google accounts.

- [Configure Azure identity provider](./secure-your-cluster/azure-idp.md)

    Integrate Azure Active Directory as an identity provider for cluster authentication.

- [Configure Azure group sync operator](./secure-your-cluster/azure-gso.md)

    Sync Azure AD groups to your cluster so group-based access control stays up to date.

- [Configure Keycloak identity provider](./secure-your-cluster/keycloak-idp.md)

    Integrate Keycloak as an identity provider for cluster authentication.

- [Configure SAML identity provider](./secure-your-cluster/saml-idp.md)

    Integrate a SAML-based identity provider for cluster authentication.

- [Review curated list of operators](./secure-your-cluster/curated-list-operators.md)

    See which operators are available and approved for installation on your cluster.

### Manage TLS certificates

- [Provision TLS certificates](./how-to-guides/certificate-management/tls-certs.md)

    Request and configure TLS certificates for your cluster using cert-manager.

- [Provision HTTP-01 challenge certificates](./how-to-guides/certificate-management/http01-certs.md)

    Use HTTP-01 ACME challenges to issue certificates for publicly accessible routes.

### Manage network

- [Configure custom domains](./networking/custom-domains.md)

    Set up custom domains for your cluster's applications and routes.

- [Configure external DNS](./networking/external-dns.md)

    Automatically manage DNS records for your cluster's services and routes.

### Manage storage

- [Expand persistent volumes](./storage/volume-expansion.md)

    Increase the size of existing persistent volume claims without downtime.

### Cluster lifecycle

- [Hibernate your cluster](./cluster-lifecycle/hibernate-your-cluster.md)

    Pause a cluster to reduce costs when it is not in use, then resume it when needed.

## Help

- [FAQ](./help/faq.md)

    Find answers to common questions about administering {{ product_name }}.
