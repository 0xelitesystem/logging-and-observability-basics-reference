# The Three Pillars

The three pillars of observability are logs, metrics, and traces, and each answers a different question about a running system. Logs are timestamped records of discrete events, metrics are numeric measurements aggregated over time, and traces follow a single request as it moves through multiple services. No single pillar is sufficient on its own; they are most powerful when correlated, so you can jump from a spiking metric to the trace that caused it to the log line that explains it. Together they cover the "what," the "where," and the "why" of system behavior.

## Logs

Logs are append-only records of discrete events, each with a timestamp, a severity, and a message or set of fields. They are the highest-detail signal and are best for answering "what exactly happened at this moment," such as an unhandled exception with a stack trace or a specific request that was rejected. Their weakness is volume and cost: logging everything is expensive to store and slow to search, so you sample or filter in high-traffic paths. Structured logs (key-value pairs rather than free text) make logs queryable and are strongly preferred.

## Metrics

Metrics are numeric measurements collected at regular intervals and aggregated, such as request rate, error rate, latency percentiles, and queue depth. They are cheap to store and fast to query because they are pre-aggregated, which makes them ideal for dashboards and alerts that need to evaluate continuously. The tradeoff is low detail: a metric tells you error rate jumped to five percent but not which requests failed or why. The four common metric types are counters, gauges, histograms, and summaries, with histograms being the right tool for latency because they preserve the distribution.

## Traces

Traces record the full path of a single request as it travels across services, breaking it into spans that each represent one unit of work with its own timing. A trace shows you that a request spent two hundred milliseconds in the auth service and then eight hundred in a slow database call, which pinpoints where latency or errors originate in a distributed system. Each span carries a trace ID and parent span ID so the pieces can be reassembled into a tree. Traces are the pillar that makes distributed systems debuggable, and standards such as OpenTelemetry give a vendor-neutral way to emit all three signal types.
