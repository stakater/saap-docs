# Sizing

> Glossary:
>
> **User workloads:** User applications (e-commerce frontend, backend APIs, etc.)
>
> **{{ product_name }} workloads:** Supporting applications for software lifecycle

## Summary

Resource requirements for a single {{ product_name }} cluster is as follows:

| Resource | Minimum | Recommended |
|:---|---:|---:|
| vCPUs (m) | 60 | 76 |
| Memory (Gib)  | 240 | 304 |
| Storage Block (Gib)| 2850 | 3450 |
| Storage Snapshots (Gib) | 330 | 330 |
| Storage Buckets (Backups) | 1 | 1 |
| Load Balancers* | 3 | 3 |
| Public/Floating IPs | 2 | 2 |

!!! note
    * Load Balancers are only required for AWS, Azure and GCP.

### Minimum

The overall minimum resource requirements are:

| Machine pool role | Minimum size (vCPU x Memory x Storage) | Minimum pool size | Total vCPUs | Total Memory (GiB) | Total Storage (GiB) |
|:---|:---|---:|---:|---:|---:|
| Control plane | 8 x 32 x 350 | 3 | 24 | 96 | 1050 (Provisioned IOPS 1000) |
| Infra | 8 x 32 x 300 | 3 | 24 | 96 | 900 (General Purpose SSD) |
| Worker | 4 x 16 x 300 | 3 | 12 | 48 | 900 (General Purpose SSD) |
| **Grand Total** | | **9** | **60** | **240** | **2850** |

### Recommended

The recommended resource requirements are:

| Machine pool role | Minimum size (vCPU x Memory x Storage) | Minimum pool size | Total vCPUs | Total Memory (GiB) | Total Storage (GiB) |
|:---|:---|---:|---:|---:|---:|
| Control plane | 8 x 32 x 350 | 3 | 24 | 96 | 1050 (Provisioned IOPS 1000) |
| Infra | 8 x 32 x 300 | 2 | 16 | 64 | 600 (General Purpose SSD) |
| Monitoring | 8 x 32 x 300 | 1 | 8 | 32 | 300 (General Purpose SSD) |
| Logging | 8 x 32 x 300 | 1 | 8 | 32 | 300 (General Purpose SSD) |
| Worker | 4 x 16 x 300 | 3 | 12 | 48 | 900 (General Purpose SSD) |
| **Grand Total** | | **10** | **68** | **272** | **3150** |

## Compute

### 3 x Control plane

The control plane manages the {{ product_name }} cluster. The control plane nodes run the control plane.

!!! note
    * No user workloads run on control plane nodes.

### 2 x Infra

At least two infrastructure nodes are required for the {{ product_name }} infrastructure workloads:

| {{ product_name }} component | vCPU requirement (m) | Memory requirement (GiB) |
|---|---:|---:|
| [Stakater Forecastle](https://github.com/stakater/Forecastle)  | 50 | 0.20 |
| [Stakater Ingress Monitor Controller](https://github.com/stakater/IngressMonitorController)  | 150 | 0.60 |
| Stakater KubeHealth ({{ product_name }} components monitoring) | 150 | 0.40 |
| [Stakater Multi Tenant Operator](https://docs.stakater.com/mto/index.html)  | 600 | 1.20 |
| [Stakater Konfigurator](https://github.com/stakater/Konfigurator) | 20 | 0.30 |
| [Stakater Reloader](https://github.com/stakater/Reloader) | 20 | 0.50 |
| [Stakater Tronador](https://docs.stakater.com/tronador/#)  | 100 | 0.20 |
| [cert-manager](https://github.com/cert-manager/cert-manager)  | 100 | 1.50 |
| [External Secrets operator](https://github.com/external-secrets/external-secrets) | 50 | 0.30 |
| [Kubernetes replicator](https://github.com/mittwald/kubernetes-replicator) | 50 | 0.30 |
| [group-sync-operator](https://github.com/redhat-cop/group-sync-operator)  | 50 | 0.10 |
| [Helm operator](https://github.com/fluxcd/helm-operator) | 500 | 0.80 |
| [Harbor](https://github.com/goharbor/harbor) | 200 | 1.60 |
| [OpenShift GitOps](https://docs.openshift.com/container-platform/4.7/cicd/gitops/understanding-openshift-gitops.html)  | 530 | 0.50 |
| [OpenShift Image Registry](https://docs.openshift.com/container-platform/4.11/registry/index.html) | 50 | 0.40 |
| [OpenShift Router](https://docs.openshift.com/container-platform/4.11/networking/ingress-operator.html)  | 300 |  0.30 |
| [OpenBao](https://github.com/openbao/openbao)  | 255 | 0.36 |
| [Velero](https://github.com/vmware-tanzu/velero)  | 500 | 0.15 |
| [Volume Expander Operator](https://github.com/redhat-cop/volume-expander-operator)  | 50 | 0.10 |
| **Total** | **4275** | **11.61** |

!!! note
    * No user workloads run on control plane nodes.

### 1 x Monitoring

Monitoring components to monitor `{{ product_name }} workloads` and user workloads are deployed on monitoring nodes. The monitoring stack is the LGTM stack (Grafana, Mimir, Loki, and Alertmanager).

Minimum one monitoring node must be used for all production deployments. For high availability consider using two monitoring nodes.

| Type of monitoring | {{ product_name }} component | vCPU requirement (m) | Memory requirement (GiB) |
|---|:---|---:|---:|
| **Infrastructure** |   |  | |
| | [Alertmanager](https://github.com/prometheus/alertmanager)   | 500 | 1.00 |
| | [Grafana](https://github.com/grafana/grafana)   | 50 | 0.10 |
| | [Node exporter](https://github.com/prometheus/node_exporter)  | 50 | 0.50 |
| | [Prometheus](https://github.com/prometheus/prometheus)   | 2500 | 7.50 |
| | [Mimir](https://github.com/grafana/mimir)   | 50 | 0.20 |
| **User Workloads** |   |  | |
| | [Alertmanager](https://github.com/prometheus/alertmanager) | 20 | 0.25 |
| | [Grafana](https://github.com/grafana/grafana) | 20 | 0.10 |
| | [Prometheus](https://github.com/prometheus/prometheus) | 100 | 2.50 |
| **Total**|    | **3290** | **12.15** |

For more details of monitoring, please visit [Creating Application Alerts](../../managed-addons/monitoring-stack/app-alerts.md).

!!! note
    * No user workloads run on control plane nodes.

### 1 x Logging (optional)

Logging components aggregate all logs and store them centrally. These components run on logging nodes. The logging stack includes the EFK stack (Elasticsearch, Fluentd and Kibana).

The logging pool is optional, if there is no need for it, it will not be deployed. Logging infrastructure is still highly recommended for troubleshooting purposes.

Minimum one logging node is required. For high availability consider using three logging nodes.

| {{ product_name }} component | vCPU requirement (m) | Memory requirement (GiB) |
|---|---:|---:|
| [Vector](https://github.com/vectordotdev/vector) (collector) | 200 | 2.0 |
| [Loki](https://github.com/grafana/loki) | 500 | 4.0 |
| **Total** | **700** | **6.0** |

!!! note
    * No user workloads run on control plane nodes.

### 3 x Worker

In a {{ product_name }} cluster, users run their applications on worker nodes. By default, a {{ product_name }} subscription comes with three worker nodes.

## Storage

### Block Storage

{{ product_name }} uses high performance disks i.e. `SSDs` for storage requirements which includes:

- Boot Volumes (attached to nodes for OS)
- Persistent Volumes (Additionally attached volumes for application consumption)

Following are the storage requirements used as Persistent Volumes consumed by `{{ product_name }} workloads`:

| {{ product_name }} component | Volume Size (GiB) |
|---|---:|
| Loki (logging) | 300  |
| Harbor | 100 |
| Mimir - Infrastructure Monitoring | 100  |
| Mimir - Workload Monitoring | 100 |
| OpenBao | 10 |
| **Total** | **610** |

### Object Storage

`1 x Object storage bucket` is required for keeping Backups of Kubernetes Objects.

### Volume Snapshot Requirements

Volume Snapshots are backups of volumes for critical `{{ product_name }} workloads` that include `Harbor` and `OpenBao`.

By default backups are taken daily and are retained for 3 days. So at a given instance 3 day old backups for `{{ product_name }} workloads` are kept.

| {{ product_name }} component | PV size | backup frequency | Backup size (GiB) |
|---|---:|---:|---:|
| Harbor | 100 | 3 | 300 |
| OpenBao | 10 | 3 | 30 |
| **Total** | | | **330** |

## Network

### Load Balancers

#### For AWS, Azure, GCP

Each {{ product_name }} cluster deploys `3 x Loadbalancers`:

- 2 x Public (for cluster API and cluster dashboard)

- 1 x Private (for control plane communication)

#### For OpenStack

No LoadBalancers required.

### Floating IPs

#### For AWS, Azure, GCP

No additional Floating IPs/Public IPs are required.

#### For OpenStack

`2 x Floating IPs` are required (for cluster API and cluster dashboard).
