# Velero

[Velero](https://github.com/vmware-tanzu/velero) backs up and restores Kubernetes workloads and persistent volumes. Use it to recover from accidental deletion, data corruption, or cluster failure, and to migrate workloads between clusters.

Backups run on a schedule and are stored in an external storage backend. A default backup location is configured for your cluster.

---

- [Backup and restore](./backup-restore.md) — back up resources and persistent volumes, restore from a backup
- [Velero CLI](./cli.md) — command reference for interacting with Velero from your terminal
- [Limitations](./limitations.md) — known constraints and unsupported scenarios
- [Cleanup](./cleanup.md) — remove backups and backup storage locations
- [Troubleshooting](./troubleshooting.md) — diagnose common Velero issues
