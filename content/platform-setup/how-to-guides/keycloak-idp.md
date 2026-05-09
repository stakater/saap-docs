# Connect Keycloak

This page explains how to federate your existing Keycloak realm into {{ product_name }} so that your users can log into the platform's managed addons with their existing accounts.

{{ product_name }} acts as a broker: you register a client in your Keycloak realm and share the credentials with Stakater Support to complete the federation.

---

## 1. Create a client in your Keycloak realm

In the realm you want to federate, create a new client with these settings:

| Setting | Value |
|---|---|
| Client ID | `ap-broker` |
| Client Protocol | `openid-connect` |
| Access Type | `Confidential` |
| Standard Flow Enabled | `ON` |
| Service Accounts Enabled | `ON` |
| Authorization Enabled | `ON` |
| Redirect URIs | Provided by Stakater Support |

---

## 2. Copy the client secret

On the newly created client, open the **Credentials** tab and copy the **Secret** value.

---

## 3. Share credentials with Stakater Support

Open a support ticket at [Stakater Support](https://support.stakater.com) and provide:

- Client ID: `ap-broker`
- Client Secret (share via a secure channel)

Stakater will complete the configuration and confirm when authentication is active.

---

With your identity provider connected, continue to [Configure authorization roles](authorization-roles.md) to set up what authenticated users can do.
