# Stakater Identity

This page explains how identity management works on {{ product_name }} and what you do to federate your own identity provider.

## How it works

Stakater operates a dedicated managed identity service — Stakater Identity — for every {{ product_name }} account. A unique realm is provisioned for your account when it is created. Your users sign in to platform applications (Forecastle, ArgoCD, Grafana, OpenBao, and so on) through this realm.

Users do not maintain credentials inside Stakater Identity. The realm federates with whichever identity provider your organisation already uses — Keycloak, Google, Azure AD, generic SAML, or OpenID Connect — so users sign in with the accounts they already have.

## What you do

Connect your existing identity provider to your realm using the matching how-to under Identity providers below. Once federation is configured, group memberships from your identity provider map to platform roles automatically; you manage users and groups in your identity provider, not in Stakater Identity itself.

## Next step

Pick the identity provider matching the system your organisation already uses and follow the per-provider setup guide.
