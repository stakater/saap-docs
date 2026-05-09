# Monitor your Application

In this tutorial, you will learn how to leverage {{ product_name }}'s built-in monitoring capabilities to observe and enhance the performance of your applications. {{ product_name }} uses powerful tools like Prometheus stack integration and Grafana, allowing you to efficiently query and visualize metrics, as well as troubleshooting and monitoring. Whether it's examining basic health indicators or diving into application-specific metrics, {{ product_name }} makes application monitoring seamless and effective. Let's dive in and explore how to supercharge your monitoring efforts with {{ product_name }}!

## Objectives

- Enable and utilize {{ product_name }}'s built-in User Workload Monitoring to observe basic health indicators of applications.

## Key Results

- Enable developers to analyze and interpret the performance and behavior of their applications through efficient monitoring.
- Centralize and streamline the monitoring process to facilitate proactive issue identification and troubleshooting.

## Tutorial

### {{ product_name }} Monitoring (pods etc.)

1. User Workload Monitoring is enabled by default in {{ product_name }}.

    Go to `{{ product_name }}` in `Developer` view, go to `Observe`, it should show basic health indicators under `<your-namespace>` Project

    ![product-review-default-metrics](images/product-review-default-metrics.png)

Great! let's now see how to expose metric for your application in next tutorial.
