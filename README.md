# LLM Dev Utilities API

Fast, deterministic text utilities for building with LLMs. Four endpoints that handle the fiddly text work so your app doesn't have to. No AI calls, no external dependencies, millisecond responses.

**Live on RapidAPI:** https://rapidapi.com/cesaricf79/api/llm-dev-utilities

Free tier included. Get your key and ready-to-paste code snippets (curl, Python, Node, PHP, and more) directly on the RapidAPI page above.

## Why

Every LLM app ends up writing the same glue code: parsing the almost-JSON a model returned, stripping timestamps out of a transcript before prompting, cutting a document down to fit the context window, or reading a wall of logs to find the actual error. These four endpoints do exactly that, predictably, with zero AI in the loop so the output never drifts.

## Endpoints

All are POST and take a JSON body with a "text" field.

- **POST /v1/json-repair** — turn messy model output into valid JSON. Fixes markdown code fences, single quotes, unquoted keys, trailing commas, Python literals (None / True / False), comments, surrounding prose, and truncated or unclosed structures. Returns the parsed object plus a list of what was changed.
- **POST /v1/srt-clean** — turn SRT or VTT captions into clean text ready to prompt with. Strips indices, timestamps and HTML tags, drops the duplicate lines auto-captions produce, and reports how many tokens you saved. Modes: plain, timed, dedupe_only.
- **POST /v1/context-compress** — shrink text to a target token budget before sending it to a model. Removes HTML and web boilerplate, deduplicates, and trims on sentence boundaries. Deterministic: it never invents content.
- **POST /v1/log-triage** — paste raw Docker, systemd or stack-trace logs and get structured triage: severity, service, exception type, message, stack head, and likely causes with concrete fixes (OOM, ECONNREFUSED, missing module, port in use, permission denied, disk full, rate limit, TLS, DB unreachable, crash loop, and more).

## Example (json-repair)

Send: a broken string such as a fenced block containing single quotes, a trailing comma and a Python-style True.

Get back: valid parsed JSON, a normalized text version, and the list of fixes applied.

Full request/response examples and per-language snippets are on the RapidAPI listing.

## Why deterministic, not "ask another model to fix it"

You could send broken JSON to a second LLM call to fix it, but that is slower, costs tokens, is non-deterministic, and can hallucinate values that were never there. Repairing JSON is a parsing problem, not a reasoning problem, so it should be solved with a parser: same input, same output, every time, in milliseconds.

## Pricing

Deliberately below market. BASIC is free; paid tiers start at $2.99/month. See current plans on the RapidAPI listing.

## License

Client examples: MIT. The hosted API is provided via RapidAPI.
