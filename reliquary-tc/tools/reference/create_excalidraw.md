---
title: "create_excalidraw"
description: "Create a new Excalidraw note via the companion plugin."
editUrl: false
---

Create a new Excalidraw note via the companion plugin. Overwriting an existing drawing requires confirmation.

| | |
|---|---|
| **Domain** | structured |
| **Scopes** | `write:excalidraw` |
| **Access** | write |
| **Tags** | `writes`, `destructive`, `hitl`, `plugin-bridge`, `domain:structured` |
| **Profile** | full only |

## Annotations {#annotations}

| Annotation | Value |
|---|---|
| Read-only | no |
| Destructive | yes |
| Idempotent | no |
| Accepts an idempotency key | no |

`Idempotent` is the advisory MCP `idempotentHint`. `Destructive` is also `yes` for a tool that
asks for confirmation only on some calls.

## Confirmation (human in the loop) {#confirmation-human-in-the-loop}

The handler asks for confirmation only when a call crosses a boundary (for example an overwrite, a folder-boundary crossing or a bulk-cost floor); other calls need none.

- The confirmation binds to the vault paths the call names, which are also checked against the folder ACL.

## Input {#input}

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `vault` | `string` |  | — | Vault id. May be omitted when only one vault is available. length 1–64; pattern `^[a-z0-9_-]+$` |
| `path` | `string` | yes | — | length 1–1024 |
| `template` | `enum` |  | — | One of: `"blank"`, `"compressed-json"`, `"custom"` |
| `elements` | `Record<string, any>[]` |  | — | — |
| `overwrite` | `boolean` |  | `false` | — |
| `elicit_token` | `string` |  | — | pattern `^[a-f0-9]{32}$` |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `path` | `string` | yes | — |
| `plugin_used` | `boolean` | yes | — |
| `unchanged` | `boolean` |  | — |
| `vault` | `string` | yes | — |

## Related tools {#related-tools}

Other tools in the `structured` domain: [`add_kanban_card`](/reliquary-tc/tools/reference/add_kanban_card/), [`create_base`](/reliquary-tc/tools/reference/create_base/), [`create_canvas`](/reliquary-tc/tools/reference/create_canvas/), [`format_table`](/reliquary-tc/tools/reference/format_table/), [`insert_table_column`](/reliquary-tc/tools/reference/insert_table_column/), [`insert_table_row`](/reliquary-tc/tools/reference/insert_table_row/), [`list_kanban_boards`](/reliquary-tc/tools/reference/list_kanban_boards/), [`move_kanban_card`](/reliquary-tc/tools/reference/move_kanban_card/), [`query_base`](/reliquary-tc/tools/reference/query_base/), [`query_canvas`](/reliquary-tc/tools/reference/query_canvas/), [`read_base`](/reliquary-tc/tools/reference/read_base/), [`read_canvas`](/reliquary-tc/tools/reference/read_canvas/), [`read_excalidraw`](/reliquary-tc/tools/reference/read_excalidraw/), [`read_kanban_board`](/reliquary-tc/tools/reference/read_kanban_board/), [`sort_table_by_column`](/reliquary-tc/tools/reference/sort_table_by_column/), [`update_base`](/reliquary-tc/tools/reference/update_base/), [`update_canvas`](/reliquary-tc/tools/reference/update_canvas/), [`update_excalidraw`](/reliquary-tc/tools/reference/update_excalidraw/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
