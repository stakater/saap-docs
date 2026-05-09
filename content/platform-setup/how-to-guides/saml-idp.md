# Connect SAML

This guide explains how to integrate a SAML 2.0 identity provider with {{ product_name }} so your users can authenticate with their existing organizational accounts.

The configuration is a two-way exchange: you register {{ product_name }} as a service provider in your IdP, and you provide Stakater Support with your IdP metadata URL to complete the federation.

---

## 1. Request the SP metadata URL

Open a support ticket at [Stakater Support](https://support.stakater.com) and request the **SAML 2.0 SP Metadata URL** for your {{ product_name }} instance. Stakater will provide this URL before you proceed.

---

## 2. Register {{ product_name }} in your identity provider

Using the SP metadata URL from step 1, register {{ product_name }} as a service provider in your IdP. The exact steps depend on your IdP, but the outcome is the same: your IdP trusts {{ product_name }} and will redirect authenticated users back to it.

Ensure your IdP is configured to include the following attributes in its SAML assertions:

| Attribute | Description |
|---|---|
| Email address | Or an equivalent unique identifier such as `eppn` |
| First name | |
| Last name | |

---

## 3. Share your IdP metadata URL with Stakater Support

Provide Stakater Support with your **SAML 2.0 IdP Metadata URL**. Stakater will complete the configuration and confirm when authentication is active.

---

With your identity provider connected, continue to [Configure authorization roles](authorization-roles.md) to set up what authenticated users can do.
