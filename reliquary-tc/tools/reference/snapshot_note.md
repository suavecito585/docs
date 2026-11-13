---
title: "snapshot_note"
description: "Capture the current content of a note as a restorable point-in-time snapshot (retained per config.snapshots.retention)."
editUrl: false
---

Capture the current content of a note as a restorable point-in-time snapshot (retained per config.snapshots.retention). Returns the snapshot id and content hash.

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
| `path` | `string` | yes | — | length 1–1024 |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `path` | `string` | yes | — |
| `snapshot_id` | `number \| null` | yes | — |
| `content_hash` | `string` | yes | — |

## Related tools {#related-tools}

Other tools in the `notes` domain: [`append_note`](/reliquary-tc/tools/reference/append_note/), [`bulk_create_notes`](/reliquary-tc/tools/reference/bulk_create_notes/), [`bulk_move_notes`](/reliquary-tc/tools/reference/bulk_move_notes/), [`copy_note`](/reliquary-tc/tools/reference/copy_note/), [`delete_note`](/reliquary-tc/tools/reference/delete_note/), [`fetch`](/reliquary-tc/tools/reference/fetch/), [`get_provenance`](/reliquary-tc/tools/reference/get_provenance/), [`list_notes`](/reliquary-tc/tools/reference/list_notes/), [`list_snapshots`](/reliquary-tc/tools/reference/list_snapshots/), [`move_note`](/reliquary-tc/tools/reference/move_note/), [`note_exists`](/reliquary-tc/tools/reference/note_exists/), [`patch_note`](/reliquary-tc/tools/reference/patch_note/), [`read_note`](/reliquary-tc/tools/reference/read_note/), [`read_notes`](/reliquary-tc/tools/reference/read_notes/), [`read_resources`](/reliquary-tc/tools/reference/read_resources/), [`read_snapshot`](/reliquary-tc/tools/reference/read_snapshot/), [`restore_note`](/reliquary-tc/tools/reference/restore_note/), [`write_note`](/reliquary-tc/tools/reference/write_note/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
