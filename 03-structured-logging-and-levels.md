# Structured Logging and Log Levels

Structured logging is the practice of emitting logs as machine-readable key-value data, typically JSON, instead of unstructured free-text strings. A structured log line like `{"level":"error","event":"payment_failed","order_id":"a1b2","amount":4200}` can be filtered, grouped, and aggregated by any field, while the string "payment failed for order a1b2" can only be grep'd. This makes logs queryable at scale and is the single highest-leverage logging habit. Pair it with consistent field names across services so a query for `order_id` works everywhere.

## Why structured beats free text

Free-text logs are written for humans reading one line at a time, but production debugging means searching millions of lines, which is a job for machines. With structured logs you can ask "show me every error event with status 500 for this user in the last hour" as a precise query instead of a fragile regex. Consistency is what unlocks this: agree on field names such as `timestamp`, `level`, `event`, `request_id`, and `service`, and attach them automatically. Most languages have a structured logging library that handles JSON encoding and context propagation for you.

## Choosing log levels

Log levels rank messages by severity so you can filter noise and route alerts, and the common ladder is DEBUG, INFO, WARN, ERROR, and FATAL. DEBUG is verbose developer detail disabled in production, INFO records normal notable events like a started job, WARN flags something recoverable but unusual, ERROR means an operation failed and likely needs attention, and FATAL means the process cannot continue. The most common mistake is logging at ERROR for things that are expected and harmless, which trains people to ignore errors. Reserve ERROR for genuine failures, and use WARN for degraded-but-handled conditions.

## Practical conventions

Set the production log level to INFO by default and make it changeable without a redeploy, ideally via an environment variable or runtime config, so you can turn on DEBUG during an incident. Always log a correlation or request ID on every line so you can stitch one request's events together across services. Include enough context in each line to act on it alone, since the reader may see only that line in a filtered view. Avoid logging in tight loops or hot paths without sampling, because log volume can itself become an outage.
