# Service Mesh

The platform's service mesh is built on [Istio](https://github.com/istio/istio). It provides mutual TLS between services, fine-grained traffic management, and per-service observability — without changes to your application code.

Mutual TLS is enforced automatically for all intra-cluster service traffic. Use the service mesh when you need traffic shifting, circuit breaking, or inter-service metrics beyond what standard Kubernetes provides.
