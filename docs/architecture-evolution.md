# Architecture Evolution

## Prototype phase

Workflow automation made it possible to validate product behavior quickly.

```text
user request
   ↓
LLM
   ↓
n8n workflow
   ↓
external systems
```

This is effective while the number of workflows, state transitions, and domain rules remains manageable.

## Product phase

As Koowky gained multi-tenancy, billing, memories, reminders, integration configuration, and richer tool behavior, core logic benefited from moving into the application backend.

```text
             ┌─ agent orchestration
             ├─ domain services
Application ─┼─ tenant isolation
             ├─ persistence
             ├─ entitlements
             └─ integration adapters
                        ↓
                 external services
```

n8n can still be valuable for integration-heavy workflows; it simply stops being the only place where business behavior lives.

## Why the change matters

Application-owned logic provides:

- version-controlled behavior
- conventional automated testing
- stronger domain boundaries
- reusable services
- clearer observability
- easier authorization enforcement
- less coupling between business logic and workflow topology

The lesson is not "low-code vs. code." It is choosing the correct ownership boundary as a product matures.
