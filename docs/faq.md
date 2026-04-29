# FAQ

## Is this repository code?

No. This repository is a public knowledge base for Claude Code, Codex, OpenAI-compatible APIs, Anthropic-compatible endpoints, subagents, tools use, and enterprise relay planning.

## Why not just use provider APIs directly?

Direct provider APIs are fine for single-user tests. Teams often need routing policy, quota handling, cost control, account isolation, fallback, and compatibility across multiple tools.

## What is the difference between OpenAI-compatible and Anthropic-compatible endpoints?

OpenAI-compatible endpoints usually expose `/v1/chat/completions` or related OpenAI-style APIs. Anthropic-compatible endpoints use Anthropic-style request and response formats. Many tools support only one shape, so using the wrong base URL can produce misleading errors.

## Does a chat completion success mean tools use will work?

No. Tools use needs tool schema, tool call IDs, assistant tool-call messages, tool result ordering, and streaming behavior to be preserved.

## Does subagent support need extra work?

Yes. Subagents often add child runtime state, delegated base URLs, separate model choices, and credential-pool isolation. A relay should not collapse all custom endpoints into one ambiguous provider label.

## Where do I try ConvertModel?

Website: <https://convertmodel.net>

New-user claim: <https://convertmodel.net/talk/claim/>

