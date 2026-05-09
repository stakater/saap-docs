# Access your cluster

This guide explains how to access the {{ product_name }} cluster via the web console and the `oc` CLI.

---

## 1. Log in via the web console

1. Go to [{{ product_name }}](https://cloud.stakater.com/) and enter the enterprise domain provided by your cluster administrator.

    ![{{ product_name }} home](images/cloud-stakater-com.png)

1. Log in using the method configured for your organization.

    ![{{ product_name }} login](images/cloud-stakater-com-login.png)

1. After login you will see the cluster overview page.

    ![Cluster management page](images/cluster-management-page.png)

1. Click the dropdown for your cluster and select **OpenShift Web Console**.

    ![OpenShift console](images/admin-view.png)

1. To view the services available on the cluster, select **Forecastle** from the same dropdown.

    ![Forecastle homepage](images/forecastle-homepage.png)

---

## 2. Log in via the CLI

1. In the OpenShift console, click your username in the top-right corner and select **Copy login command**.

    ![Copy login command](images/copy-login-command.png)

1. Click **Display token**.

    ![Display token](images/display-token.png)

1. Copy the login command and run it in your terminal:

    ```bash
    oc login --token=<TOKEN> --server=<SERVER>
    ```

---

With cluster access confirmed, continue to [Deploy a demo app](../../deploy-demo-app.md) to deploy your first application.
