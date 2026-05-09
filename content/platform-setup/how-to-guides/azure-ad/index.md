# Azure AD

Integrating Azure AD lets your users log in to {{ product_name }} with their existing corporate credentials and gives your team automatic access based on the Azure AD security groups they already belong to.

There are two steps. The first is required; the second is optional but strongly recommended for any team larger than a handful of people.

| Step | Guide | When you need it |
|---|---|---|
| 1 | [Connect Azure AD](../azure-idp.md) | Required — enables Azure AD login for all users |
| 2 | [Configure Azure AD group sync](../azure-gso.md) | Recommended — maps Azure AD groups to platform roles automatically |

---

## Connect Azure AD

Registering {{ product_name }} as an application in your Azure AD tenant allows users to authenticate with their corporate accounts. Without this step, users must be created and managed manually inside the platform.

Complete this step first — group sync depends on it.

---

## Configure Azure AD group sync

Once Azure AD login is working, group sync removes the need to assign platform roles by hand. When a user logs in, their Azure AD group memberships are read and translated into the appropriate platform roles automatically.

Set this up if your team uses Azure AD security groups to manage access, or if you want role changes in Azure AD to be reflected in the platform without manual intervention.

---

Start with [Connect Azure AD](../azure-idp.md), then return here to set up [group sync](../azure-gso.md).
