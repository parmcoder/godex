# Project Conventions

Prefer this shape for new services when no project convention exists:

```text
cmd/service-name/
internal/
  <domain>/
  platform/
  transport/http/
pkg/
```

Rules:

- Split packages by domain or adapter responsibility, not by vague layers like `utils`.
- Keep `main` thin: load config, build dependencies, start the service, handle shutdown.
- Put config structs in `config.go`.
- Put shared constants and package-level variables in `const.go` when they must exist.
- Keep one main struct per file where practical; do not split tiny cohesive code just to satisfy the rule.
- Keep interfaces close to consumers.
- Keep database, cache, Kafka, and HTTP transport details out of domain logic.
- Use `internal/` for service-private code.
- Use `pkg/` only for intentionally reusable public libraries.
- Keep generated files reproducible and clearly marked.

Before editing, inspect package docs, filenames, tests, `go.mod`, task files, and existing dependency patterns.
