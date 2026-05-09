# OpenTelemetry

OpenTelemetry is the observability instrumentation layer on the platform. It collects traces, metrics, and logs from your applications and routes them to the appropriate backends — Tempo for traces, Mimir for metrics, Loki for logs.

Instrument your application with an OpenTelemetry SDK and emit spans. The platform's OpenTelemetry Collector receives and forwards them automatically — your application does not connect to Tempo or Loki directly.
