# Development Workflows

Prefer Taskfile for common commands. Keep commands boring, named, and reproducible.

Useful tasks:

- `task test`: run unit tests
- `task test:integration`: run dependency-backed tests
- `task lint`: run formatting and lint checks
- `task run`: start the service locally
- `task docs`: rebuild Swagger docs
- `task mocks`: regenerate mockery mocks
- `task wire`: regenerate Wire providers
- `task dev`: run with Air
- `task debug`: run with Delve

Docker development image:

- Include Go toolchain, Air, and Delve when local container debugging is useful.
- Keep production image separate from debug tooling.
- Document exposed debug ports and security implications.

Generated outputs:

- Make Swagger, mockery, and Wire regeneration explicit.
- Keep generated files deterministic.
- Verify generated docs stay consistent with API changes.
