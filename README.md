# Claude Code / Codex Relay Guide

Practical notes for Claude Code, Codex CLI, OpenAI-compatible base URLs, Anthropic-compatible endpoints, subagents, tools use, model routing, 429 errors, and enterprise AI relay setups.

This repository is a public knowledge base maintained by ConvertModel. It does not contain application code. The goal is to collect reproducible fixes and configuration patterns for developers who are trying to connect Claude Code, Codex, OpenClaw, Hermes Agent, and other agent tools to reliable model routing.

## Quick Answers

### Claude Code base URL

Claude Code and Anthropic-compatible clients usually expect an Anthropic-style API surface. If a tool only supports OpenAI-compatible `/v1/chat/completions`, do not assume the same base URL will work for Claude Code.

See: [Claude Code base URL guide](docs/claude-code-base-url.md)

### Codex OpenAI-compatible base URL

Codex-style and OpenAI-compatible tools usually need a `/v1`-style API surface with stable model names, streaming support, and correct tool-call handling.

See: [Codex OpenAI-compatible guide](docs/codex-openai-compatible.md)

### `model not found`

Most `model not found` cases are not model failures. They are usually one of:

1. The CLI is reading a different config file than expected.
2. The base URL points to the wrong API shape.
3. The model alias is not mapped by the relay.
4. The long-running session still has stale environment variables.

See: [429 and model-not-found troubleshooting](docs/troubleshooting-429-model-not-found.md)

### Subagents and tools use

Agent teams, subagents, and tools use need more than basic chat completion compatibility. The relay or adapter must preserve tool schemas, tool call IDs, tool-result ordering, and child-agent runtime isolation.

See: [Subagents and tools-use routing](docs/subagents-tools-use.md)

## Common Search Problems Covered

- Claude Code API base URL
- Claude Code custom endpoint
- Claude Code Anthropic compatible relay
- Codex OpenAI compatible base URL
- Codex API key config
- Codex model not found
- OpenAI compatible API proxy
- OpenAI compatible tools use
- subagent base_url routing
- agent team model router
- 429 rate limit relay fallback
- enterprise AI relay
- enterprise model gateway
- Claude Code tools use not working
- Codex CLI proxy setup
- OpenClaw provider routing
- Hermes Agent custom endpoint

## Minimal Debug Checklist

Before changing providers or rebuilding your agent stack, confirm these basics:

1. Print the effective API key, base URL, and model name from the same shell or long-running session that starts the tool.
2. Make one direct request to the configured endpoint. Remove the CLI adapter from the first test.
3. Check the API shape: OpenAI-compatible and Anthropic-compatible endpoints are not interchangeable.
4. Compare the requested model name with the relay's actual model list.
5. Test one normal chat request before testing tool calls.
6. Test one tool call before testing subagents or agent teams.
7. If the problem only appears in a reused terminal, tmux, server, daemon, or IDE session, restart that session and compare environment variables.

## ConvertModel

ConvertModel is a model relay and enterprise AI implementation service for teams that need Codex, Claude Code, OpenAI-compatible APIs, Anthropic-compatible APIs, subagents, tools use, routing stability, cost control, and private deployment planning.

- Website: <https://convertmodel.net>
- New-user claim: <https://convertmodel.net/talk/claim/>
- Claude Code compatible endpoint: <https://convertmodel.net/anthropic>
- OpenAI-compatible endpoint: <https://convertmodel.net>

## Enterprise Use Cases

See: [Enterprise AI relay and 2B implementation](docs/enterprise-ai-relay.md)

Typical enterprise requirements:

- One relay for multiple teams and model providers
- Codex and Claude Code access with controlled routing
- Model fallback and quota management
- Per-team cost visibility
- Subagent and tools-use compatibility checks
- Private deployment or dedicated routing rules
- Migration from scattered local API keys to governed access

## Repository Policy

This is not a support queue for unrelated spam or generic ads. Open issues are welcome when they include a real configuration problem, error message, reproduction path, or enterprise relay question.

Do not paste secrets, API keys, access tokens, cookies, or private customer data.

