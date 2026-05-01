# How many clusters do you need?

The right number of clusters depends on your organization's workload criticality, team structure, and operational requirements. This page covers the common patterns to help you decide.

## Life cycle stages: development, testing, production

Most organizations separate workloads across at least three clusters:

1. **Development** — a sandbox for experimentation. Multiple small, short-lived clusters work better than a single shared one, but a single sandbox cluster is acceptable.
1. **Testing** — validates patches, configuration changes, and upgrades before they reach production. Some organizations call this pre-production.
1. **Production** — runs live workloads.

For non-critical applications, you can reduce this to two clusters (combining development and testing) or even one. A single cluster can use separate namespaces for each stage, but carries more risk:

- A patch that affects the whole cluster could introduce production issues that a dedicated test environment would have caught first.
- Runaway workloads in development (excessive container creation, disk usage) can impact production.

There is no single correct number — look at how similar applications in your organization handle staging to find the right baseline.

## Business continuity and disaster recovery

Many organizations run a second production cluster in a different cloud region as a failover (Disaster Recovery, DR). This protects against a full cluster or region failure.

{{ product_name }} provides a 99.5% uptime SLA, which is sufficient for most business-critical applications. If your application requires higher availability — such as 99.999% — you can achieve a composite SLA by running multiple {{ product_name }} clusters simultaneously, either within the same region or across regions.
