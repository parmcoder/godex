# Observability

Logging:

- Use `log/slog`.
- Add useful keys: service, operation, request ID, trace ID, dependency, duration, status.
- Do not log secrets, tokens, connection strings, PII, raw credentials, or sensitive payloads.
- Avoid noisy success logs. Log state changes, failures, degraded dependency behavior, and audit-relevant events.

Tracing and metrics:

- Use Go OpenTelemetry.
- Support Jaeger for local and deployed tracing.
- Add spans around important external calls and business operations.
- Add span attributes that help debug without exposing sensitive values.
- Propagate trace context through HTTP and messaging boundaries.
- Include request IDs or trace IDs in logs where possible.

Health:

- Keep liveness, readiness, and metrics behavior aligned with Kubernetes.
- Readiness should reflect dependencies required to serve traffic.
