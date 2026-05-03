# Reloader

Reloader watches ConfigMaps and Secrets for changes and automatically rolls the pods that depend on them. Without Reloader, updating a ConfigMap does not restart the pods that reference it — the new value only takes effect on the next manual rollout.

Annotate your workload once and Reloader handles rolling updates automatically whenever the referenced resource changes.

---

- [Configure Reloader annotations](./tutorial/configure-resources.md) — enable auto-detection or watch specific ConfigMaps and Secrets
