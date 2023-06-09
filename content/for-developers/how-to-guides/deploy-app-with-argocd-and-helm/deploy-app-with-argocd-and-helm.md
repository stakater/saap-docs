
# Deploy Application with ArgoCD and Helm

We will cover application deployment with Helm and ArgoCD in this section.

## Deploy your Application with Helm

Let's deploy a simple application using Helm. Helm charts are packaged and stored in repositories. They can be added as dependencies of other charts or used directly. Let's add a chart repository now. The chart repository stores the version history of our charts as well as the packaged tar file.

We created and packaged a Helm chart to the Nexus Helm Repository available in Stakater App Agility Platform (SAAP)

1. From your Terminal, add the Nexus Helm Repository using the following command. Consider the

    ```bash
    helm repo add NEXUS_HELM_REPO_NAME NEXUS_HELM_REPO_URL
    ```

1. Install a chart from this repo. Start by searching the repository to see what is available.

    ```bash
    helm search repo stakater-nordmart-review
    ```

1. Now install the latest version. Helm likes to give each install its own release.

    ```bash
    helm install RELEASE_NAME NEXUS_HELM_REPO_NAME/takater-nordmart-review --namespace ${TENANT_NAME}-dev
    ```

1. Open the application up in the browser to verify it's up and running. Here's a handy one-liner to get the URL of the app.

    ```bash
    oc project ${TENANT_NAME}-dev
    oc get pods,svc -n ${TENANT_NAME}-dev
    ```

1. Run the following command to port forward the pod to your local machine and run curl command to verify your application is running and serving requests.

     ```sh
     # get podname with oc get
     oc port-forward <podname> 8080:8080
     curl localhost:8080/api/review/329199
     ```

1. You can upgrade your chart values with CLI. By default, your application has only 1 replica. You can view this using the following command.

     ```bash#test
     oc get pods -n ${TENANT_NAME}-dev
     ```

    By default, there is one replica of your application. Let's use Helm to set this to 5.

    ```bash#test
    helm upgrade RELEASE_NAME NEXUS_HELM_REPO_NAME/APP_NAME --set APP_NAME.deployment.replicas=5 --namespace ${TENANT_NAME}-dev
    ```

    Verify the deployment has scaled up to 5 replicas.

    ```bash#test
    oc get pods -n ${TENANT_NAME}-dev
    ```

1. If you're done playing with the `Nordmart Review API`. You can tidy up your work by removing the chart. To do this, run `helm uninstall` to remove your release of the chart.

    ```bash#test
    helm uninstall stakater-nord -namespace ${TENANT_NAME}-dev
    ```

    Verify the cleanup.

    ```bash#test
    oc get pods -n ${TENANT_NAME}-dev
    ```

## Deploy your Application with ArgoCD

1. Log into ArgoCD UI.

1. Lets deploy a sample application through the UI. In fact, let's get ArgoCD to deploy the `stakater-nordmart-review` app you manually deployed previously using Helm. On ArgoCD - click `+ NEW APP`. You should see an empty form. Let's fill it out by setting the following:

      - On the **GENERAL** box

         - Application Name: `<TENANT_NAME>-nordmart-review`
         - Project: `<TENANT_NAME>` (select the project corresponding to your `<TENANT_NAME>` from the `project` dropdown)
         - Sync Policy: `Automatic`

      - On the **SOURCE** box

         - Repository URL: `NEXUS_HELM_REGISTRY_URL`
         - Select `Helm` from the right dropdown menu
         - Chart: `stakater-nordmart-review`
         - Version: `1.0.0`

      - On the **DESTINATION** box

         - Cluster URL: `https://kubernetes.default.svc`
         - Namespace: `<TENANT_NAME>-test`

    Your form should look like the follow image, if so click `Create`

1. After you hit `Create`, you'll see `<TENANT_NAME>-nordmart-review` application is created and should start deploying in your `<TENANT_NAME>-test` namespace.

1. If you drill down into the application you will get ArgoCD's amazing view of all k8s resources that were generated by the chart

1. You can verify the application is running and behaving as expected by navigating to `Workloads` > `Pods` section in the `<TENANT_NAME-test` namespace in your `OpenShift Console`.

      > Select the dropdown menu and switch to `Administrator` view in the OpenShift console if you are not already there

1. Run the following command to port forward the pod to your local machine and run curl command to verify your application is running and serving requests.

     ```sh
     # get podname with oc get
     oc port-forward <podname> 8080:8080
     curl localhost:8080/api/review/329199
     ```
