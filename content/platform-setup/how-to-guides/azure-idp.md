# Connect Azure AD as an identity provider

This page explains how to register an Azure AD application and share the credentials with Stakater Support so that users in your Azure AD tenant can log into {{ product_name }}.

Azure AD requires two separate app registrations: one for identity (this page) and one for [group synchronization](azure-gso.md). Complete the identity registration first.

---

## 1. Register an application in Azure AD

1. Log in to the [Azure Portal](https://portal.azure.com).
1. Open the **Azure Active Directory** service.
1. Under **Manage**, click **App registrations**, then **New registration**.
1. Enter `{{ product_name_lower }}` as the name.
1. Under **Redirect URI**, select `Web` and enter the URI provided by Stakater Support.
1. Click **Register**.

![Azure AD app registration](images/azure-ad.png)

---

## 2. Add API permissions

Go to **API permissions** for the newly created app and add the following Microsoft Graph permissions:

- `User.Read`
- `openid`
- `profile`
- `email`

---

## 3. Create a client secret

1. Click **Certificates & secrets** in the left sidebar.
1. Click **New client secret**.
1. Enter `{{ product_name_lower }}-oidc` as the description, choose an expiry, and click **Add**.
1. Copy the **Value** of the new secret immediately — it will not be shown again.

![Certificates and secrets](images/azure-ad-certificates-secrets.png)

---

## 4. Share the credentials with Stakater Support

From the app registration **Overview** tab, note the **Application (client) ID** and **Directory (tenant) ID**. Send these to Stakater Support via a secure channel along with the client secret:

- Application (client) ID
- Directory (tenant) ID
- Client secret

![Client and tenant IDs](images/azure-ad-clientid-tenantid.png)

---

With the identity provider registration complete, continue to [Configure Azure group sync](azure-gso.md) to synchronize your Azure AD groups into {{ product_name }}.
