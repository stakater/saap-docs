# Cert-Manager

[Cert-Manager](https://github.com/cert-manager/cert-manager) automates TLS certificate issuance and renewal. It provisions certificates from Let's Encrypt, HashiCorp Vault, or a private PKI, and rotates them automatically before expiry — no manual certificate management required.

Routes and Ingresses on the platform are secured by adding a `cert-manager.io/issuer-name` annotation to the resource. Cert-Manager detects the annotation, requests the certificate, and injects the TLS configuration automatically.

---

To configure TLS for your applications:

- [Configure TLS certificates](../../platform-setup/how-to-guides/tls-certs.md) — DNS-01 challenges, wildcard certificates, custom domains
- [Use http-01 certificate challenges](../../platform-setup/how-to-guides/http01-certs.md) — single hostnames without DNS credentials
