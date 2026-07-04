# Configuration

Environment config default:

- Use `github.com/caarlos0/env`.
- Set `envDefault` for safe defaults.
- Set `required` tags for mandatory values.
- Keep structs in `config.go`.
- Validate after loading and return clear errors.

Complex config:

- Use YAML when config is hierarchical or operationally large.
- Keep YAML structs explicit; avoid untyped `map[string]any` except at edges.
- Validate manually after loading.
- Fail fast before starting listeners or workers.

Rules:

- Do not log secret values.
- Prefer explicit durations, URLs, pool sizes, and feature flags.
- Keep config defaults boring and safe for local development.
- Let deployment supply production values.
