# FAQs

## Why do we reserve memory/CPU on each node?

An OpenShift/Kubernetes Node consist system services that ensure the smooth running of cluster e.g. kubelet, KubeAPIServer and other OS processes/services. Workloads running on these nodes can starve system services of CPU time or trigger Out of Memory (OOM) exceptions. To prevent these issues, a small chunk of resources needs to be permanently allocated to these services so they can run smoothly.
To fully utilize resources. An automatic script calculates and allocates CPU/memory resources according to the node utilization. For more details see [capacity reservation docs](https://docs.openshift.com/container-platform/latest/nodes/nodes/nodes-nodes-resources-configuring.html#nodes-nodes-resources-configuring-auto_nodes-nodes-resources-configuring) for OpenShift.
