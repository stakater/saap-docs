# User access (SSO)

Users who log in via OAuth external identity providers have no permissions by default. You can grant a user one of two types of permissions:

- [Customer Admin](#customer-admin)
- [Tenant level permissions](#tenant-level-permissions)

## Customer Admin

Customer Admin is an administrator-level role with restrictive access. A user with this role can:

- Create/Manage/Delete Tenants
- Read cluster status (Overview page)
- Administrate non-managed Projects/Namespaces
- Install/Modify/Delete operators in non-managed Projects/Namespaces

To assign this role, open a [support ticket](https://support.stakater.com/index.html) with the username or email of the user.

## Tenant level permissions

These permissions are granted per Tenant and are restricted to the tenant's Namespaces/Projects. For a detailed explanation of these roles see [Tenant Member Roles](https://docs.stakater.com/mto/main/tenant-roles.html).

A [Customer Admin](#customer-admin) grants tenant level permissions by creating or editing the *Tenant* CR.

To grant tenant level permissions see the detailed example for [Tenant CR](https://docs.stakater.com/mto/main/customresources.html#2-tenant).

## Configure identity provider for your cluster

### Social identity providers

A social identity provider delegates authentication to a trusted social media account. Red Hat Single Sign-On supports Google, Facebook, Twitter, GitHub, LinkedIn, Microsoft, and Stack Overflow.

- [Configure Azure AD identity provider](./azure-idp.md)
- [Configure a Keycloak identity provider](./keycloak-idp.md)
- [Configure a SAML identity provider](./saml-idp.md)
- [Configure a Google identity provider](./google-idp.md)
