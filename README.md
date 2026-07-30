# Logging and Observability Basics

This reference is a plain-language guide to logging and observability for working developers. It covers the three pillars (logs, metrics, and traces), how to write structured logs, how to pick log levels, what data must never be logged, and how to build alerts that fire on real problems. The goal is correctness and practical habits you can apply to any service.

## The core idea

Observability is the property of a system that lets you understand its internal state from the outside by examining the data it emits, namely its logs, metrics, and traces. A system is observable when you can answer new questions about its behavior without shipping new code to expose more data. This differs from monitoring, which watches a fixed set of known conditions, because observability is meant to help you investigate unknown problems you did not predict. The three signal types are complementary: metrics tell you something is wrong, traces tell you where, and logs tell you why. Good observability is designed in, not bolted on after an outage.

## What is inside

- [01-what-observability-is.md](01-what-observability-is.md) defines observability, contrasts it with monitoring, and explains why it matters.
- [02-three-pillars.md](02-three-pillars.md) breaks down logs, metrics, and traces and when to reach for each.
- [03-structured-logging-and-levels.md](03-structured-logging-and-levels.md) covers structured (key-value) logging and how to choose log levels.
- [04-what-not-to-log.md](04-what-not-to-log.md) lists the PII, secrets, and sensitive data you must keep out of logs.
- [05-alerting-basics.md](05-alerting-basics.md) explains symptom-based alerting, thresholds, and reducing noise.

## The stance

This reference favors structured logging over free-text strings, symptom-based alerts over cause-based ones, and a strict default of never logging secrets or personal data. It treats traces and metrics as first-class signals rather than afterthoughts. Where a practice trades convenience for safety, this guide picks safety, because a leaked credential in a log file is far more expensive than a slightly harder debugging session.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright 0xelitesystem 2026.
