# Vertical Pod Autoscaler

VPA automatically adjusts the CPU and memory requests on your pods based on actual usage. When a pod consistently uses more or less than its requested resources, VPA updates the requests to match — reducing over-provisioning and preventing resource starvation.

VPA applies changes by restarting pods with the updated requests, so it works best for workloads that tolerate occasional restarts.
