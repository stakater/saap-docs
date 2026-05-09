# Configure authorization roles

{{ product_name }} provides two roles that control what users can do on your cluster: **Customer Admin** and **Tenant member**. Assign the right role based on what each person needs to do.

---

## Customer Admin

Customer Admin has elevated access across all customer-owned namespaces. Assign this role to platform administrators who manage tenants, quotas, operators, and cluster-wide resources.

### Permissions

#### Operators

- Can view OperatorHub in the console
- Can install operators in customer-owned namespaces
- Can create, view, and delete CRs for curated operators
- Can install cluster-wide operators from the curated OperatorHub list
- Cannot install privileged or custom operators cluster-wide

#### Namespaces

- Can create, update, and patch customer-owned namespaces
- Can create, view, edit, and delete all resources in customer-owned namespaces
- Can view (not modify) resources in platform-managed namespaces

#### Storage

- Can create, view, and edit persistent volume claims, storage classes, and volume snapshots
- Cannot delete persistent volume claims, storage classes, or volume snapshots

#### Networking

- Can create, view, and delete `NetworkPolicy` objects in customer-owned namespaces
- Can view services, routes, and ingresses in all namespaces
- Can view and update DNS resources in customer-owned namespaces

#### Monitoring

- Can view the console dashboard with namespace metrics
- Can view events in all namespaces

#### Compute

- Can view machines, nodes, and machine config pools
- Cannot delete or modify machines, nodes, or machine config pools

#### User management

- Can view users and groups
- Can create and view service accounts, roles, and role bindings in customer-owned namespaces
- Can assign `admin` and `edit` role bindings in customer-owned namespaces
- Cannot add or remove cluster-admin members

#### Backups

- Can create, view, edit, and delete Velero backup and restore resources
- Can manage Velero schedules

#### Administration

- Can create, edit, and delete resource quotas and limit ranges
- Can access the `customer-admin` project to create service accounts with elevated privileges

### How to request Customer Admin

Open a [support ticket](https://support.stakater.com) with the email address of the user to assign.

---

## Tenant member

Tenant member permissions are scoped to a single tenant's namespaces. The available roles within a tenant (viewer, editor, owner) are defined by Multi Tenant Operator.

A Customer Admin grants tenant-level access by editing the `Tenant` CR. See [Tenant member roles](https://docs.stakater.com/mto/main/tenant-roles.html) for the full role breakdown.

---

Continue to [Configure user access](user-access.md) to assign these roles to your users.
