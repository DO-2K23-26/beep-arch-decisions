-> Observability

A full observability stack is very complex to handle, and very resource hungry, but also very important in case of issues.

--> Health

I suggest all apps implement the 3 kubernetes probes Liveness, Readiness and Startup.

--> Logs

Define a standardized logs format between apps, in json, and written to standard output - taking security practices into account for the logs format definition.

Logs: Alloy -> Loki

--> Tracing

Traces : OTel Collector (/!\ Rust support) -> Tempo

We may use a Service Mesh to automatically propagate trace IDs into requests - although that means more complex setup and maintenance of the cluster.

--> Metrics

Prometheus Operator -> Mimir

--> Visualization and alerting

Grafana (datasources Mimir, Loki, Tempo)

For disks, smartmontools with alerts sent to Grafana.

Long-term storage:

Configure with backups on CEPH. Aggregate metrics of interest.
