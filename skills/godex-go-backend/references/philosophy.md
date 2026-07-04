# Philosophy

Use Go as Go:

- Prefer clear data flow, explicit errors, small functions, and standard library primitives.
- Reach for the standard library before a dependency. For web servers, start with `net/http`.
- Use composition-first design. Encapsulate state and behavior with structs and methods when it clarifies ownership.
- Add interfaces only at boundaries that need substitution, usually near the consumer.
- Avoid generic infrastructure layers until there are at least two real use cases.
- Keep package APIs stable when code may be imported by another module. Treat exported names as a contract.
- Prefer deletion and simplification over new configuration, hooks, or plugin points.

Do not fight the existing repo. If a project already has a coherent pattern, extend it unless it creates a real production risk.
