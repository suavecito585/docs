---
title: "add_vault"
description: "Register a new vault at runtime (no restart)."
editUrl: false
---

Register a new vault at runtime (no restart). Validates the path is an existing directory, adds it to the registry, and indexes it for search. Runtime-only — add it to the config file to persist across restarts.

| | |
|---|---|
| **Domain** | vault |
| **Scopes** | `admin:vault` |
| **Access** | write |
| **Tags** | `read-only`, `admin`, `domain:vault` |
| **Profile** | core, full |

## Annotations {#annotations}

| Annotation | Value |
|---|---|
| Read-only | yes |
| Destructive | no |
| Idempotent | no |
| Accepts an idempotency key | no |

`Idempotent` is the advisory MCP `idempotentHint`. `Destructive` is also `yes` for a tool that
asks for confirmation only on some calls.

## Confirmation (human in the loop) {#confirmation-human-in-the-loop}

No human confirmation is required to call this tool.

## Input {#input}

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `vault_id` | `string` | yes | — | length 1–64; pattern `^[a-z0-9_-]+$` |
| `path` | `string` | yes | — | length ≥ 1 |
| `name` | `string` |  | — | length ≥ 1 |
| `kind` | `enum` |  | `"private"` | One of: `"private"`, `"docs"`, `"system"` |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `id` | `string` | yes | — |
| `name` | `string` | yes | — |
| `path` | `string` | yes | — |
| `indexed` | `boolean` | yes | — |
| `index` | `object \| null` | yes | — |
| `index.notes_seen` | `integer` | yes | range ≥ -9007199254740991 |

## Related tools {#related-tools}

Other tools in the `vault` domain: [`get_vault`](/reliquary-tc/tools/reference/get_vault/), [`index_vault`](/reliquary-tc/tools/reference/index_vault/), [`list_vaults`](/reliquary-tc/tools/reference/list_vaults/), [`refresh_plugin_capabilities`](/reliquary-tc/tools/reference/refresh_plugin_capabilities/), [`reload_vault`](/reliquary-tc/tools/reference/reload_vault/), [`reset_vault_cache`](/reliquary-tc/tools/reference/reset_vault_cache/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
