# Connect SAML

This page explains how to integrate a SAML v2.0 identity provider with {{ product_name }} so your users can authenticate with their existing organizational accounts.

The configuration is coordinated with Stakater Support: you provide your SAML metadata URL, and Stakater provides the SP metadata URL for your identity provider to trust.

---

## Prerequisites

Your SAML identity provider must expose the following attributes in its assertions:

- Email address (or an equivalent unique identifier such as `eppn`)
- First name
- Last name

---

## Steps

1. Contact Stakater Support to receive the **SAML 2.0 SP Metadata URL** for your {{ product_name }} instance.
1. Register {{ product_name }} as a service provider in your identity provider using the SP metadata URL.
1. Provide Stakater Support with your **SAML 2.0 IdP Metadata URL** so the integration can be completed.

---

With your identity provider connected, continue to [Configure authorization roles](authorization-roles.md) to set up what authenticated users can do.
