---
title: "makemd_query"
description: "Forward a make.md space query through the companion bridge."
editUrl: false
---

Forward a make.md space query through the companion bridge. Current make.md releases expose no query API, so the companion reports make.md as unreachable; `sort`, `limit` and `cursor` are not passed to make.md.

| | |
|---|---|
| **Domain** | automation |
| **Scopes** | `read:makemd` |
| **Access** | read |
| **Tags** | `read-only`, `plugin-bridge`, `domain:automation` |
| **Profile** | full only |

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
| `vault` | `string` |  | — | Vault id. May be omitted when only one vault is available. length 1–64; pattern `^[a-z0-9_-]+$` |
| `space_id` | `string` | yes | — | length ≥ 1 |
| `filter` | `Record<string, any>` |  | — | — |
| `sort` | `Record<string, any>` |  | — | — |
| `limit` | `integer` |  | `50` | range 1–1000 |
| `cursor` | `string` |  | — | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `space_id` | `string` | yes | — |
| `items` | `any[]` | yes | — |
| `total` | `integer` | yes | range ≥ -9007199254740991 |

## Related tools {#related-tools}

Other tools in the `automation` domain: [`bundle_files`](/reliquary-tc/tools/reference/bundle_files/), [`bundle_folder`](/reliquary-tc/tools/reference/bundle_folder/), [`eval_dataview_field`](/reliquary-tc/tools/reference/eval_dataview_field/), [`execute_command`](/reliquary-tc/tools/reference/execute_command/), [`execute_template`](/reliquary-tc/tools/reference/execute_template/), [`generate_uri`](/reliquary-tc/tools/reference/generate_uri/), [`list_commands`](/reliquary-tc/tools/reference/list_commands/), [`list_quickadd_actions`](/reliquary-tc/tools/reference/list_quickadd_actions/), [`list_tasks`](/reliquary-tc/tools/reference/list_tasks/), [`list_templates`](/reliquary-tc/tools/reference/list_templates/), [`makemd_list_spaces`](/reliquary-tc/tools/reference/makemd_list_spaces/), [`remotely_save_status`](/reliquary-tc/tools/reference/remotely_save_status/), [`remotely_save_trigger`](/reliquary-tc/tools/reference/remotely_save_trigger/), [`show_file_in_obsidian`](/reliquary-tc/tools/reference/show_file_in_obsidian/), [`tasks_filter`](/reliquary-tc/tools/reference/tasks_filter/), [`trigger_quickadd`](/reliquary-tc/tools/reference/trigger_quickadd/), [`update_task`](/reliquary-tc/tools/reference/update_task/), [`validate_dql`](/reliquary-tc/tools/reference/validate_dql/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
