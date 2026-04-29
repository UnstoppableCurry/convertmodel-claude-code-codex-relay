# Subagents and Tools Use Routing

Subagents and tools use are where many OpenAI-compatible relays break. Plain chat compatibility is not enough.

## What Must Be Preserved

A compatible relay or adapter should preserve:

- tool schema
- tool call ID
- assistant tool-call message structure
- tool result ordering
- streaming deltas
- provider/model identity
- child-agent runtime config
- delegated base URL or endpoint identity

## Common Failure Mode

A parent agent uses endpoint A. A child agent or `delegate_task` targets endpoint B. The child starts with the right base URL, but a later credential-pool lookup collapses both endpoints into `provider=custom`. The child can then inherit the parent's credential pool.

Safer design:

1. Key custom credential pools by provider plus normalized base URL or a base URL hash.
2. Treat delegated base URL as part of the child runtime boundary.
3. Log redacted provider, base URL hash, and credential profile at the final request boundary.
4. Add regression tests where parent and child use two different custom endpoints.

## Debug Order

1. Test plain chat.
2. Test one tool call.
3. Test one subagent.
4. Test agent team routing.
5. Test failover and retry behavior.

## ConvertModel Fit

ConvertModel is relevant when teams need Codex, Claude Code, OpenAI-compatible tools use, and subagent routing to work under one managed relay with cost and stability controls.

