# Configure user access

Users who log in via your identity provider have no permissions by default. This page explains how to grant the two types of access available in {{ product_name }}.

---

## Customer Admin

Customer Admin is an administrator-level role with access across all customer-owned namespaces. A user with this role can:

- Create, manage, and delete tenants
- Read cluster status from the overview page
- Manage non-platform namespaces and operators

To assign this role, open a [support ticket](https://support.stakater.com/index.html) with the username or email of the user.

---

## Tenant-level access

Tenant-level permissions are scoped to the namespaces belonging to a specific tenant. A Customer Admin grants these permissions by editing the `Tenant` CR.

For the available roles (viewer, editor, owner) and what each allows, see [Tenant member roles](https://docs.stakater.com/mto/main/tenant-roles.html).

For a worked example of granting tenant access, see [Tenant CR reference](https://docs.stakater.com/mto/main/customresources.html#2-tenant).

---

Your platform bootstrap is now complete. To deploy your first application, continue to [Deploy](../../develop/tutorials/deploy-demo-app.md). For custom routing and TLS, see [Configure custom domains](custom-domains.md).
