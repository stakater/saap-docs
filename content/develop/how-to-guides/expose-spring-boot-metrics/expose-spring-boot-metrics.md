# Expose metrics from a Spring Boot application

This guide shows you how to instrument a Spring Boot application so that its metrics are sent to {{ product_name }} and visible in Grafana.

## How it works

The OpenTelemetry Spring Boot starter emits JVM, web server, and database metrics as soon as it is on the classpath. You point the SDK at the in-cluster OTel collector through your `values.yaml` for the [Stakater Application Helm Chart](../../../managed-addons/helm-leader-chart/index.md); the platform receives the metrics over OTLP and stores them in Mimir.

## 1. Add the OpenTelemetry Spring Boot starter

Add the starter to your `pom.xml`:

```xml
<dependency>
    <groupId>io.opentelemetry.instrumentation</groupId>
    <artifactId>opentelemetry-spring-boot-starter</artifactId>
</dependency>
```

JVM, web server, and database metrics are emitted automatically once the starter is on the classpath.

## 2. Point the SDK at the in-cluster OTel collector

Set the OTel SDK environment variables in your application's `values.yaml` for the Stakater Application Helm Chart:

```yaml
deployment:
  env:
    - name: OTEL_SERVICE_NAME
      value: your-service-name
    - name: OTEL_EXPORTER_OTLP_ENDPOINT
      value: http://otel-collector.observability.svc.cluster.local:4317
    - name: OTEL_METRICS_EXPORTER
      value: otlp
```

Commit the change; ArgoCD applies it; metrics appear in Grafana within a minute.

## 3. Add a custom metric

The OpenTelemetry API lets you register counters, gauges, and histograms in code. The example below registers a counter that increments every time a review receives a rating of three or below:

```java
import io.opentelemetry.api.GlobalOpenTelemetry;
import io.opentelemetry.api.metrics.LongCounter;
import io.opentelemetry.api.metrics.Meter;

private final Meter meter = GlobalOpenTelemetry.getMeter("nordmart-review");
private final LongCounter ratingCounter = meter
    .counterBuilder("nordmart.review.low_ratings")
    .setDescription("Total number of ratings below 3")
    .build();

public void recordRating(int rating) {
    if (rating <= 3) {
        ratingCounter.add(1);
    }
}
```

The counter appears in Grafana as `nordmart_review_low_ratings_total` once the first rating is recorded.

## Next step

Continue to [Logs](../../../managed-addons/logging/index.md) to forward your application logs to the platform.
