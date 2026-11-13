---
title: "list_notes"
description: "List notes under a folder (read-ACL filtered), with cursor pagination."
editUrl: false
---

List notes under a folder (read-ACL filtered), with cursor pagination. response_format=concise returns \{vault, notes: [\{path\}], next_cursor\}, without size, mtime, folder and total_returned.

| | |
|---|---|
| **Domain** | notes |
| **Scopes** | `read:notes` |
| **Access** | read |
| **Tags** | `read-only`, `domain:notes` |
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
| `vault` | `string` |  | — | Vault id. May be omitted when only one vault is available. length 1–64; pattern `^[a-z0-9_-]+$` |
| `folder` | `string` |  | — | length 1–1024 |
| `recursive` | `boolean` |  | `true` | — |
| `extensions` | `string[]` |  | — | — |
| `response_format` | `enum` |  | — | concise returns only the high-signal fields; detailed (the shipped default) returns the full payload. Errors and safety warnings are never trimmed. When omitted, the server's tools.defaults.responseFormat applies. One of: `"concise"`, `"detailed"` |
| `verbosity` | `enum` |  | — | Legacy alias for response_format: terse = concise, full = detailed. One of: `"full"`, `"terse"` |
| `limit` | `integer` |  | — | range 1–1000 |
| `cursor` | `string` |  | — | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `folder` | `string` |  | — |
| `notes` | `object[]` | yes | — |
| `notes[].path` | `string` | yes | — |
| `notes[].size` | `number` |  | — |
| `notes[].mtime` | `number` |  | — |
| `next_cursor` | `string \| null` | yes | — |
| `total_returned` | `number` |  | — |

## Related tools {#related-tools}

Other tools in the `notes` domain: [`append_note`](/reliquary-tc/tools/reference/append_note/), [`bulk_create_notes`](/reliquary-tc/tools/reference/bulk_create_notes/), [`bulk_move_notes`](/reliquary-tc/tools/reference/bulk_move_notes/), [`copy_note`](/reliquary-tc/tools/reference/copy_note/), [`delete_note`](/reliquary-tc/tools/reference/delete_note/), [`fetch`](/reliquary-tc/tools/reference/fetch/), [`get_provenance`](/reliquary-tc/tools/reference/get_provenance/), [`list_snapshots`](/reliquary-tc/tools/reference/list_snapshots/), [`move_note`](/reliquary-tc/tools/reference/move_note/), [`note_exists`](/reliquary-tc/tools/reference/note_exists/), [`patch_note`](/reliquary-tc/tools/reference/patch_note/), [`read_note`](/reliquary-tc/tools/reference/read_note/), [`read_notes`](/reliquary-tc/tools/reference/read_notes/), [`read_resources`](/reliquary-tc/tools/reference/read_resources/), [`read_snapshot`](/reliquary-tc/tools/reference/read_snapshot/), [`restore_note`](/reliquary-tc/tools/reference/restore_note/), [`snapshot_note`](/reliquary-tc/tools/reference/snapshot_note/), [`write_note`](/reliquary-tc/tools/reference/write_note/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
