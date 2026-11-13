---
title: "fetch"
description: "Fetch one note by the id a search result returned and return {id, title, text, url, metadata}: the full note text (frontmatter included), an absolute citation url, and metadata {vault, path, conten..."
editUrl: false
---

Fetch one note by the id a search result returned and return \{id, title, text, url, metadata\}: the full note text (frontmatter included), an absolute citation url, and metadata \{vault, path, content_hash, modified\}. Refuses a note the caller may not read exactly as read_note does.

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
| `id` | `string` | yes | — | length 1–1100 |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `id` | `string` | yes | — |
| `title` | `string` | yes | — |
| `text` | `string` | yes | — |
| `url` | `string` | yes | — |
| `metadata` | `object` | yes | — |
| `metadata.vault` | `string` | yes | — |
| `metadata.path` | `string` | yes | — |
| `metadata.content_hash` | `string` | yes | — |
| `metadata.modified` | `string` |  | — |

## Related tools {#related-tools}

Other tools in the `notes` domain: [`append_note`](/reliquary-tc/tools/reference/append_note/), [`bulk_create_notes`](/reliquary-tc/tools/reference/bulk_create_notes/), [`bulk_move_notes`](/reliquary-tc/tools/reference/bulk_move_notes/), [`copy_note`](/reliquary-tc/tools/reference/copy_note/), [`delete_note`](/reliquary-tc/tools/reference/delete_note/), [`get_provenance`](/reliquary-tc/tools/reference/get_provenance/), [`list_notes`](/reliquary-tc/tools/reference/list_notes/), [`list_snapshots`](/reliquary-tc/tools/reference/list_snapshots/), [`move_note`](/reliquary-tc/tools/reference/move_note/), [`note_exists`](/reliquary-tc/tools/reference/note_exists/), [`patch_note`](/reliquary-tc/tools/reference/patch_note/), [`read_note`](/reliquary-tc/tools/reference/read_note/), [`read_notes`](/reliquary-tc/tools/reference/read_notes/), [`read_resources`](/reliquary-tc/tools/reference/read_resources/), [`read_snapshot`](/reliquary-tc/tools/reference/read_snapshot/), [`restore_note`](/reliquary-tc/tools/reference/restore_note/), [`snapshot_note`](/reliquary-tc/tools/reference/snapshot_note/), [`write_note`](/reliquary-tc/tools/reference/write_note/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
