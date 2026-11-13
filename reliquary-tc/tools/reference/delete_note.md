---
title: "delete_note"
description: "Delete a note (to the vault's .trash mirror, or permanently)."
editUrl: false
---

Delete a note (to the vault's .trash mirror, or permanently). Destructive — requires confirmation. restore_note reads its undo from a snapshot, which is captured only when the server's snapshots.enabled config is on; the default "trusted-local" posture leaves it on, so a deleted note has a restore_note path back unless snapshots have been explicitly disabled.

| | |
|---|---|
| **Domain** | notes |
| **Scopes** | `delete:notes` |
| **Access** | destructive |
| **Tags** | `writes`, `destructive`, `hitl`, `domain:notes` |
| **Profile** | core, full |

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

A single-use `elicit_token` (or a transport-verified confirmation) is required on every call.

- The confirmation binds to the vault paths the call names, which are also checked against the folder ACL.

## Input {#input}

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `vault` | `string` |  | — | Vault id. May be omitted when only one vault is available. length 1–64; pattern `^[a-z0-9_-]+$` |
| `path` | `string` | yes | — | length 1–1024 |
| `permanent` | `boolean` |  | `false` | — |
| `prev_hash` | `string` |  | — | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `path` | `string` | yes | — |
| `deleted` | `boolean` | yes | — |
| `permanent` | `boolean` | yes | — |
| `trashed_to` | `string \| null` | yes | — |
| `prev_hash` | `string \| null` | yes | — |

## Related tools {#related-tools}

Other tools in the `notes` domain: [`append_note`](/reliquary-tc/tools/reference/append_note/), [`bulk_create_notes`](/reliquary-tc/tools/reference/bulk_create_notes/), [`bulk_move_notes`](/reliquary-tc/tools/reference/bulk_move_notes/), [`copy_note`](/reliquary-tc/tools/reference/copy_note/), [`fetch`](/reliquary-tc/tools/reference/fetch/), [`get_provenance`](/reliquary-tc/tools/reference/get_provenance/), [`list_notes`](/reliquary-tc/tools/reference/list_notes/), [`list_snapshots`](/reliquary-tc/tools/reference/list_snapshots/), [`move_note`](/reliquary-tc/tools/reference/move_note/), [`note_exists`](/reliquary-tc/tools/reference/note_exists/), [`patch_note`](/reliquary-tc/tools/reference/patch_note/), [`read_note`](/reliquary-tc/tools/reference/read_note/), [`read_notes`](/reliquary-tc/tools/reference/read_notes/), [`read_resources`](/reliquary-tc/tools/reference/read_resources/), [`read_snapshot`](/reliquary-tc/tools/reference/read_snapshot/), [`restore_note`](/reliquary-tc/tools/reference/restore_note/), [`snapshot_note`](/reliquary-tc/tools/reference/snapshot_note/), [`write_note`](/reliquary-tc/tools/reference/write_note/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
