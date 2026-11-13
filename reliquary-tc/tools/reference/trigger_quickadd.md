---
title: "trigger_quickadd"
description: "Fire a QuickAdd action by name."
editUrl: false
---

Fire a QuickAdd action by name. Always requires human confirmation (execute:quickadd is a HITL floor): actions can create or modify notes broadly and run macros.

| | |
|---|---|
| **Domain** | automation |
| **Scopes** | `execute:quickadd` |
| **Access** | write |
| **Tags** | `writes`, `hitl`, `plugin-bridge`, `domain:automation` |
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

A single-use `elicit_token` (or a transport-verified confirmation) is required on every call.

- The effect is opaque, so the confirmation binds to the argument hash alone.

## Input {#input}

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `vault` | `string` |  | — | Vault id. May be omitted when only one vault is available. length 1–64; pattern `^[a-z0-9_-]+$` |
| `action_name` | `string` | yes | — | length ≥ 1 |
| `args` | `Record<string, any>` |  | — | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `action_name` | `string` | yes | — |
| `fired_at` | `string` | yes | — |

## Related tools {#related-tools}

Other tools in the `automation` domain: [`bundle_files`](/reliquary-tc/tools/reference/bundle_files/), [`bundle_folder`](/reliquary-tc/tools/reference/bundle_folder/), [`eval_dataview_field`](/reliquary-tc/tools/reference/eval_dataview_field/), [`execute_command`](/reliquary-tc/tools/reference/execute_command/), [`execute_template`](/reliquary-tc/tools/reference/execute_template/), [`generate_uri`](/reliquary-tc/tools/reference/generate_uri/), [`list_commands`](/reliquary-tc/tools/reference/list_commands/), [`list_quickadd_actions`](/reliquary-tc/tools/reference/list_quickadd_actions/), [`list_tasks`](/reliquary-tc/tools/reference/list_tasks/), [`list_templates`](/reliquary-tc/tools/reference/list_templates/), [`makemd_list_spaces`](/reliquary-tc/tools/reference/makemd_list_spaces/), [`makemd_query`](/reliquary-tc/tools/reference/makemd_query/), [`remotely_save_status`](/reliquary-tc/tools/reference/remotely_save_status/), [`remotely_save_trigger`](/reliquary-tc/tools/reference/remotely_save_trigger/), [`show_file_in_obsidian`](/reliquary-tc/tools/reference/show_file_in_obsidian/), [`tasks_filter`](/reliquary-tc/tools/reference/tasks_filter/), [`update_task`](/reliquary-tc/tools/reference/update_task/), [`validate_dql`](/reliquary-tc/tools/reference/validate_dql/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
