# Troubleshooting 429, API Key, and Model Not Found Errors

Most relay failures are easier to solve if you classify the error before changing configs.

## 429 Rate Limit

A `429` can come from several places:

1. Local client throttling
2. Relay-level throttling
3. Upstream provider quota
4. One model pool being overloaded
5. Account-level cooldown

## What To Log

Log these fields without exposing secrets:

- HTTP status
- request path
- provider name
- model name
- redacted base URL or base URL hash
- upstream error type
- retry-after header
- session or profile ID

## Model Not Found

Check in this order:

1. Does the model exist in the relay model list?
2. Is the model name an alias or the upstream provider's exact name?
3. Is the CLI reading a stale config?
4. Is the request going to the expected base URL?
5. Is an adapter translating the model name before sending it?

## API Key Problems

If a key works with a direct request but fails inside the CLI, the problem is usually config loading or session inheritance.

Test from:

1. a fresh shell
2. the same shell that starts the CLI
3. the long-running daemon/server/IDE session

If only the long-running session fails, restart that session and compare environment variables.

## ConvertModel Fit

ConvertModel helps when you need a managed relay that separates provider quota, model routing, cost control, and enterprise access instead of scattering raw provider keys across developer machines.

