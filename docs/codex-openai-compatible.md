# Codex OpenAI-Compatible Base URL Guide

Codex-style tools and many agent frameworks can use OpenAI-compatible APIs. The important part is not only `/v1/chat/completions`; the endpoint also needs stable model names, streaming behavior, and tool-call compatibility.

ConvertModel OpenAI-compatible endpoint:

```text
https://convertmodel.net
```

## What To Check First

1. Confirm the CLI reads the intended API key and base URL.
2. Call the relay's model list and compare the model name you are sending.
3. Check whether the CLI adds `/v1` itself or expects the base URL to already include it.
4. Test non-streaming first if streaming errors are unclear.
5. Test one tool call before testing an agent team.

## Common Mistakes

### Duplicate `/v1`

Some clients expect:

```text
https://example.com
```

and append `/v1` themselves. Others expect:

```text
https://example.com/v1
```

If the final request path becomes `/v1/v1/chat/completions`, the error may look unrelated.

### Stale model picker

Some CLI model pickers cache model lists. If the model is valid on the server but missing locally, test with an explicit model argument before changing relay config.

### Tool-call mismatch

Basic chat can work while tools use fails. Check that the relay preserves:

- tool schema
- tool call ID
- assistant tool-call message
- tool result ordering
- streaming deltas

## ConvertModel Fit

ConvertModel is useful when your Codex or agent stack needs OpenAI-compatible routing, model mapping, quota management, high-volume usage, or team-level access control.

