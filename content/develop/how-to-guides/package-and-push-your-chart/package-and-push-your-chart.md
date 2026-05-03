# Package and push your chart to Harbor

## Objectives

- Push artifacts to Harbor Registry hosted on {{ product_name }}.

## Key Results

- Helm chart package and pushed to Harbor.

## Guide

### Get Harbor Helm Registry URL

## Docker Image and Helm Chart Repository hosted by Harbor

> Ask admin Helm Registry Credentials for helm chart repository.

Find Harbor Helm Registry URL the Harbor registry URL (find it in Forecastle).

Alternatively, Navigate to the cluster Forecastle, search `nexus` using the search bar on top menu and copy the nexus URL.

- `nexus-helm-reg-url` : Add `-helm` in URL after `nexus` and append `/repository/helm-charts/`. This URL points to Helm Registry referred as `nexus-helm-reg-url` in this tutorial for example `https://nexus-helm-stakater-nexus.apps.clustername.random123string.kubeapp.cloud/repository/helm-charts/`

    ![nexus-Forecastle](../images/nexus-forecastle.png)

### Package and Upload the chart to Harbor

1. Run the following command to package the helm chart into compressed file.

   ```sh
   # helm package [CHART_PATH]
   helm package .
   ```

   This command packages a chart into a versioned chart archive file.

1. Upload packaged chart to Harbor Helm Registry.

   ```sh
   curl -u "<helm_user>":"<helm_password>" `nexus-helm-reg-url` --upload-file "CHART_NAME-CHART_VERSION.tgz"
   ```

   > Make sure to get credentials from Stakater Admin.

1. Open Harbor UI from Forecastle. Upon opening the link, you'll be redirected to Harbor home page.

    ![`nexus-Forecastle`](../images/nexus-forecastle.png)
    ![`nexus-homepage`](../images/nexus-homepage.png)

1. Select `Browse` from the left sidebar, Click on `Helm Charts` to view your Helm Registry Charts.

    ![`nexus-browse-helm`](../images/nexus-browse-helm.png)

1. Verify that the chart you uploaded is present in the list.

    ![`nexus-helm-charts`](../images/nexus-helm-charts.png)
