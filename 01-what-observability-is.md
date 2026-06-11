# What Observability Is

Observability is the ability to understand a system's internal state by examining the external data it produces, without needing to add new instrumentation to answer each new question. The term comes from control theory, where a system is observable if its internal state can be inferred from its outputs. In software, that output is telemetry: logs, metrics, and traces. The practical test is whether you can debug a novel production problem using data you already collect, rather than guessing and redeploying.

## Observability versus monitoring

Monitoring watches a predefined set of conditions and tells you when a known threshold is crossed, while observability is built to explore problems you did not anticipate. Monitoring answers "is the thing I expected to break, broken?" Observability answers "why is this behaving strangely, and I have no idea where to start?" You need both: monitoring gives you dashboards and alerts for known failure modes, and observability gives you the raw, high-cardinality data to investigate the unknown ones. A system can be heavily monitored yet barely observable if all its telemetry is pre-aggregated and low in detail.

## Why it matters

Modern systems are distributed, asynchronous, and full of failure modes that no one predicted at design time. When a request crosses ten services, a single error message tells you little without the surrounding context of which service, which user, and which downstream call failed. Observability shortens the time from "users are complaining" to "here is the exact line and condition that broke," which is the metric that actually matters during an incident. The cost of poor observability is paid in long outages and in engineers staring at logs that do not contain the answer.

## High cardinality and context

The power of observability comes from carrying rich, high-cardinality context through your telemetry, such as request IDs, user IDs (hashed), region, version, and feature flags. Cardinality refers to the number of distinct values a field can take; a user ID has very high cardinality, while a status code has low cardinality. High-cardinality fields let you slice data to find that a bug only affects one customer on one app version in one region. Design your telemetry to attach this context consistently so you can filter and group by it later.
