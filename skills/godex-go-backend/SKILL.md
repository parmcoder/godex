---
name: godex-go-backend
description: Use when working on Go backend services: build, review, test, debug, refactor, or production-harden HTTP APIs, pgx repositories, Redis caches, Kafka/Sarama consumers, OpenTelemetry/Jaeger observability, Swagger docs, Google Wire dependency injection, mockery tests, Taskfile workflows, Air/Delve debugging, Kubernetes readiness, or Go package structure.
---

# Godex Go Backend

## Core Rule

Act like a pragmatic Go backend engineer. Inspect first, reuse existing project conventions, use the standard library when it holds, and add the smallest production-grade change that solves the real problem.

## Quick Workflow

1. Use `gopls`-backed navigation when available: inspect definitions, references, call sites, interfaces, and package boundaries before editing.
2. Read the local code shape before applying Godex defaults. Existing clear conventions win.
3. Prefer idiomatic Go, explicit errors, `context.Context` on I/O, composition-first design, and small interfaces near consumers.
4. Use YAGNI: no speculative frameworks, factories, generic repositories, or interfaces with one implementation.
5. For uncertain library behavior, fetch current docs first with `ctx7` or official documentation. Do not guess API syntax.
6. Make behavior testable before adding implementation. Prefer TDD for small, clear units.
7. Verify with the narrowest useful command, then broaden when touching shared behavior.

## Non-Negotiables

- Never log secrets, tokens, connection strings, PII, raw credentials, or sensitive payloads.
- Use `log/slog` for structured logging and keep logs operationally useful, not noisy.
- Use Kubernetes-friendly `/healthz`, `/readyz`, and `/metricz` for services.
- Validate config after loading and fail fast with clear errors.
- Use context-aware database, cache, HTTP, and Kafka operations.
- Keep generated mocks, Swagger docs, and Wire providers reproducible through project tasks.
- Keep dependency choices boring: stdlib first, existing dependencies second, Godex defaults only when the project has no established choice.

## Reference Routing

Read only what the task needs:

| Task | Read |
| --- | --- |
| Go design, YAGNI, package versioning | `references/philosophy.md` |
| Project layout, package boundaries, file naming | `references/project-conventions.md` |
| HTTP server, probes, handlers, Swagger | `references/web-server.md` |
| Env or YAML config | `references/configuration.md` |
| Unit, suite, mockery, integration tests | `references/testing.md` |
| Code review | `references/code-review.md` |
| PostgreSQL or transactions | `references/database.md` |
| Redis or cache behavior | `references/cache.md` |
| Kafka or Sarama | `references/kafka.md` |
| Logs, traces, metrics, Jaeger | `references/observability.md` |
| Taskfile, Air, Delve, local workflows | `references/development-workflows.md` |
| Kubernetes and release readiness | `references/production-readiness.md` |
| Final review gates | `references/checklists.md` |
| User-facing workflow examples | `references/examples.md` |
| Release maturity and future work | `references/roadmap.md` |

## Default Library Choices

Use these only when the project has no established alternative:

| Need | Default |
| --- | --- |
| Env config | `github.com/caarlos0/env` |
| PostgreSQL | `github.com/jackc/pgx` |
| Redis | `github.com/redis/go-redis` |
| Kafka | `github.com/IBM/sarama` |
| Telemetry | Go OpenTelemetry with Jaeger |
| API docs | `github.com/swaggo/swag` |
| Mocks | `mockery` |
| Dependency injection | Google Wire |
| Developer tasks | Taskfile |
| Local debug image | Air and Delve |

## Output Expectations

When acting with this skill:

- State which project conventions you found and which Godex defaults apply.
- Keep changes scoped to the package or behavior under work.
- Add or update the smallest useful tests for new logic.
- Mention any doc lookup performed for library-specific behavior.
- Report exact verification commands and results.
