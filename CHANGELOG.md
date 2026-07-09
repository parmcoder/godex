# Changelog

## 0.0.3

- Added safe pgx transaction-ownership guidance for repository and service boundaries.
- Added a transaction decision table, service-owned transaction example, external side-effect patterns, and PostgreSQL integration-test requirements.

## 0.0.2

- Tightened Go backend testing guidance with separate CI-safe unit/service tests and local-only integration tests.
- Added explicit guidance for `httpmock`, `pgxmock`, `redismock`, Sarama mocks, and generated mockery mocks at external boundaries.
- Added PostgreSQL, Redis, Kafka, and HTTP/API integration-test expectations, including setup/teardown and test data populators.
- Added stock/inventory repository coverage expectations for real PostgreSQL transaction and invariant behavior.

## 0.0.1

- Initialized Godex as an independent Codex plugin.
- Added the `godex-go-backend` skill for Go backend engineering.
- Added reference docs for web servers, configuration, testing, databases, cache, Kafka, observability, production readiness, examples, and roadmap.
- Set project licensing to Apache-2.0.
