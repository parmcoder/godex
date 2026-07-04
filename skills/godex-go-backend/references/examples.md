# Examples

Use these as prompt patterns.

## Review Existing Service

```text
Use $godex-go-backend to review this Go service for package structure, tests, config validation, observability, and Kubernetes readiness.
```

Expected behavior: inspect with `gopls` where available, read existing conventions, then report production risks before style issues.

## Scaffold New Service

```text
Use $godex-go-backend to plan a minimal Go HTTP service with net/http, env config, health/readiness/metrics endpoints, slog, and Taskfile commands.
```

Expected behavior: plan the smallest service shape; do not generate a broad framework unless asked.

## Add Health, Readiness, Metrics

```text
Use $godex-go-backend to add Kubernetes-friendly /healthz, /readyz, and /metricz endpoints to this service.
```

Expected behavior: keep liveness cheap, readiness dependency-aware, and metrics consistent with existing observability.

## Add pgx Repository

```text
Use $godex-go-backend to add a pgx-backed repository with explicit SQL, clear transaction boundaries, and cancellation tests.
```

Expected behavior: read current database patterns first and avoid a generic repository abstraction.

## Add Redis Cache

```text
Use $godex-go-backend to add a go-redis cache for this lookup with documented key format, TTL, miss behavior, and outage behavior.
```

Expected behavior: centralize keys and make failure behavior explicit.

## Add Sarama Consumer

```text
Use $godex-go-backend to add an IBM Sarama consumer with graceful shutdown, idempotent handling, tracing, and explicit offset commits.
```

Expected behavior: document delivery tradeoffs and avoid payload logging.

## Add OpenTelemetry and Jaeger

```text
Use $godex-go-backend to add OpenTelemetry traces and Jaeger support to this Go service.
```

Expected behavior: fetch current docs before library-specific setup and add useful, safe span attributes.

## Generate Swagger Docs

```text
Use $godex-go-backend to add swaggo/swag docstrings and a Taskfile command that rebuilds Swagger docs for frontend consumers.
```

Expected behavior: keep docs reproducible and consistent with API changes.

## Generate Mockery Tests

```text
Use $godex-go-backend to add tests for this component using mockery-generated mocks only where mocks are justified.
```

Expected behavior: prefer plain tests unless mocks add value.

## Debug with Air and Delve

```text
Use $godex-go-backend to add local debug workflow notes for Air hot reload and Delve debugging.
```

Expected behavior: keep debug tooling out of production images.
