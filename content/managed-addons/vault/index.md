# OpenBao

OpenBao is the secrets management service for the platform. It stores API keys, database credentials, certificates, and other sensitive data in a centralized, access-controlled store. Applications retrieve secrets at runtime through the External Secrets Operator rather than having them hard-coded in configuration.

Each tenant has a dedicated path in OpenBao. Access is governed by policies that match your platform roles.
