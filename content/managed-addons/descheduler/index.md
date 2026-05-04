# Descheduler

The Descheduler continuously rebalances pod placement after initial scheduling. The Kubernetes scheduler places pods when they are first created but does not move them if cluster conditions change — the Descheduler fills that gap by evicting pods from suboptimal nodes so they are rescheduled to better ones.

Common triggers include underutilized nodes, changed affinity or taint rules, node failure, and pods crash-looping. Critical pods, daemonset pods, and pods with local storage are never evicted.
