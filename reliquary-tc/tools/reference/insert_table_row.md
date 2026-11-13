---
title: "insert_table_row"
description: "Insert a data row into a GFM table."
editUrl: false
---

Insert a data row into a GFM table. `values` are cell strings (padded/truncated to the column count); `at` is the 0-based data-row position (default: append).

| | |
|---|---|
| **Domain** | structured |
| **Scopes** | `write:notes` |
| **Access** | write |
| **Tags** | `writes`, `domain:structured` |
| **Profile** | full only |

## Annotations {#annotations}

| Annotation | Value |
|---|---|
| Read-only | no |
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
| `vault` | `string` |  | — | Vault id. May be omitted when only one vault is available. length 1–64; pattern `^[a-z0-9_-]+$` |
| `path` | `string` | yes | — | length 1–1024 |
| `table_index` | `integer` |  | `0` | range ≥ 0 |
| `values` | `string[]` | yes | — | — |
| `at` | `integer` |  | — | range ≥ 0 |
| `prev_hash` | `string` |  | — | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `path` | `string` | yes | — |
| `table_index` | `integer` | yes | range ≥ -9007199254740991 |
| `rows` | `integer` | yes | range ≥ -9007199254740991 |
| `columns` | `integer` | yes | range ≥ -9007199254740991 |
| `content_hash` | `string` | yes | — |
| `prev_hash` | `string` | yes | — |
| `redactions` | `number` |  | — |
| `conventions` | `object` |  | — |
| `conventions.warnings` | `object[]` |  | — |
| `conventions.warnings_omitted` | `integer` |  | range ≥ -9007199254740991 |
| `conventions.file_warnings` | `object[]` |  | — |
| `conventions.file_warnings_omitted` | `integer` |  | range ≥ -9007199254740991 |

## Related tools {#related-tools}

Other tools in the `structured` domain: [`add_kanban_card`](/reliquary-tc/tools/reference/add_kanban_card/), [`create_base`](/reliquary-tc/tools/reference/create_base/), [`create_canvas`](/reliquary-tc/tools/reference/create_canvas/), [`create_excalidraw`](/reliquary-tc/tools/reference/create_excalidraw/), [`format_table`](/reliquary-tc/tools/reference/format_table/), [`insert_table_column`](/reliquary-tc/tools/reference/insert_table_column/), [`list_kanban_boards`](/reliquary-tc/tools/reference/list_kanban_boards/), [`move_kanban_card`](/reliquary-tc/tools/reference/move_kanban_card/), [`query_base`](/reliquary-tc/tools/reference/query_base/), [`query_canvas`](/reliquary-tc/tools/reference/query_canvas/), [`read_base`](/reliquary-tc/tools/reference/read_base/), [`read_canvas`](/reliquary-tc/tools/reference/read_canvas/), [`read_excalidraw`](/reliquary-tc/tools/reference/read_excalidraw/), [`read_kanban_board`](/reliquary-tc/tools/reference/read_kanban_board/), [`sort_table_by_column`](/reliquary-tc/tools/reference/sort_table_by_column/), [`update_base`](/reliquary-tc/tools/reference/update_base/), [`update_canvas`](/reliquary-tc/tools/reference/update_canvas/), [`update_excalidraw`](/reliquary-tc/tools/reference/update_excalidraw/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
