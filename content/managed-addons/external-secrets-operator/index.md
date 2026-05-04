# External Secrets Operator

External Secrets Operator syncs secrets from OpenBao — and supported cloud secret stores such as AWS Secrets Manager, Azure Key Vault, and GCP Secret Manager — into Kubernetes Secrets. Your application reads a standard Kubernetes Secret; ESO handles fetching and rotating the value from the source.

Define an `ExternalSecret` resource in your namespace and ESO reconciles it automatically. The Stakater Application Helm Chart exposes this as `application.externalSecret` in your `values.yaml`.
