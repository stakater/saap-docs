# Custom Metrics Autoscaler

The Custom Metrics Autoscaler extends horizontal scaling beyond CPU and memory to any custom or external metric — queue depth, request latency, active connections, or anything your application exposes. It also supports scaling to zero, which is not possible with the standard Horizontal Pod Autoscaler.

Use it when your scaling signal is application-level or comes from an external system such as a message queue or event stream.
