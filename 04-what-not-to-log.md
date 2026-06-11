# What Not to Log

Never log secrets, credentials, or personally identifiable information (PII), because logs are widely accessible, long-lived, and copied into many downstream systems where a single leak becomes permanent. Logs are routinely shipped to third-party aggregators, replicated to backups, and read by on-call engineers who should not see customer data. Treat your log pipeline as an untrusted, broadly readable surface and scrub sensitive fields before they are ever written. The safest default is an allowlist of fields you log, not a blocklist of fields you redact.

## Secrets and credentials

Passwords, API keys, access tokens, session cookies, private keys, and database connection strings must never appear in logs, not even at DEBUG level. A common leak is logging an entire HTTP request or response object, which silently includes the Authorization header and any token in the body. Another is logging a full exception that serializes config containing credentials. Redact these at the source by maintaining a deny-list of header and field names (authorization, cookie, password, token, secret) that your logging layer strips automatically.

## Personal and regulated data

PII includes names, email addresses, phone numbers, physical addresses, government IDs, full payment card numbers, and precise location, and much of it is regulated under laws such as GDPR and CCPA. Logging it creates compliance liability and expands the blast radius of any breach. When you need to correlate by user, log a stable hashed or tokenized identifier instead of the raw value, so you keep debuggability without storing the personal data itself. For payment cards, never log the full PAN; at most log the last four digits, which is what PCI DSS permits.

## How to prevent leaks

Prevention works best as automatic infrastructure rather than developer discipline, because someone will eventually forget. Build redaction into a shared logging wrapper that recognizes sensitive field names and replaces values with a marker like `[REDACTED]`. Add a pre-write filter or linter that scans for patterns resembling tokens, card numbers, and emails. Periodically audit a sample of production logs for sensitive data, and ensure log retention is bounded so old data does not accumulate risk indefinitely.
