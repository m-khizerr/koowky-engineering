# Multi-Tenancy & Agent Safety

## Tenant context first

The active tenant should be resolved before an agent receives business tools.

```ts
type TenantContext = {
  userId: string;
  tenantId: string;
  role: string;
  entitlements: string[];
};
```

Illustrative only; this is not production source code.

## Defense in depth

Tenant isolation should not rely on one filter in one layer.

Useful boundaries include:

- authenticated membership
- tenant-scoped repository queries
- domain authorization
- tenant-scoped tool execution
- credential ownership
- audit metadata

## Tool minimization

An agent should receive only the tools relevant to the current authenticated context.

For example, if a tenant's plan does not include a capability, the corresponding tool can be omitted or rejected server-side.

## Secrets

Provider API keys and tenant credentials belong in secret storage.

They should not be:

- inserted into LLM prompts
- logged in plaintext
- returned through tool results
- exposed to browser code unnecessarily

## High-impact actions

For actions with meaningful external consequences, a system can require explicit confirmation before execution.

The broader principle is that natural-language convenience should not weaken normal application security controls.
