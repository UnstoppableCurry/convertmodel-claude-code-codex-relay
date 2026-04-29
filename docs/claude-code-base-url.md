# Claude Code Base URL Guide

Claude Code routing problems often look like authentication errors, unavailable models, or tool-use failures. The first thing to separate is API shape.

## Key Point

Claude Code and Anthropic-compatible clients usually expect an Anthropic-style endpoint. OpenAI-compatible `/v1/chat/completions` endpoints are useful for many tools, but they are not automatically compatible with Claude Code.

ConvertModel exposes an Anthropic-compatible Claude Code path at:

```text
https://convertmodel.net/anthropic
```

## Debug Flow

1. Confirm which config file Claude Code is reading.
2. Print the active base URL from the exact shell/session that starts Claude Code.
3. Confirm whether the endpoint is Anthropic-compatible or OpenAI-compatible.
4. Restart long-running terminals, IDE sessions, daemons, or tmux sessions after changing environment variables.
5. Test a simple chat request before testing subagents or tools.

## Symptoms

Common symptoms of a wrong base URL shape:

- `model not found`
- `401` or `403` even when the key is valid
- streaming starts but fails mid-response
- tool calls appear in the wrong format
- subagents work in one provider path but fail in another

## Safer Test

Use a clean session. Set only the minimum key/base/model variables, then run one simple prompt. If that works, add tools and subagents after the base route is proven.

## ConvertModel Fit

ConvertModel is relevant when you need a Claude Code-compatible relay, multi-account routing, enterprise control, or a fallback path that does not require every developer to manage local provider keys.

