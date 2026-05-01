# Hibernate your cluster

For clusters running non-critical workloads — such as test or development environments, or clusters only used during business hours — you can schedule cluster hibernation to reduce cloud costs under a pay-as-you-go model.

Cluster Hibernation automatically powers your cluster nodes (including control plane nodes) up or down according to your defined cron schedule.

It takes around 1-3 minutes to take your cluster offline and about 3-5 minutes to power back up depending on your cloud provider.

## Schedule hibernation for your cluster

You can schedule a hibernation window for non-critical workload clusters using cron jobs from your web console.

To configure a Hibernation Schedule, go to your Cluster Management page where you can view all your managed clusters.

![clusters](./images/{{ product_name }}-clusters.png)

Click on the menu button beside the cluster for which you wish to set a hibernation window and select Manage `Power State`.

![manage_powerstate_1](./images/manage-powerstate-1.png)

**Hibernating Schedule** accepts a cron expression which specifies when to power your cluster down. E.g a cron expression of “0 20 ** *” will power your cluster down at 8pm  every day.

**Running Schedule** accepts a cron expression which specifies when to power  your cluster up. E.g a cron expression of “0 8 ** *” will power your cluster up at 8am every day.

**cron Schedule** allows you to enable or disable a cron schedule.

**Power State** allows you to manually select a Power State for your cluster. You can set it to Running or Hibernation.

Setting your Power State to Hibernation will immediately power your cluster down, while Running will bring back your cluster online.

![manage_poerstate2](./images/manage-powerstate2.png)

