---
title: "add_tag"
description: "Add a tag to a note's frontmatter `tags` list or inline in the body (idempotent)."
editUrl: false
---

Add a tag to a note's frontmatter `tags` list or inline in the body (idempotent). Domain: metadata.

| | |
|---|---|
| **Domain** | metadata |
| **Scopes** | `write:notes` |
| **Access** | write |
| **Tags** | `writes`, `domain:metadata` |
| **Profile** | core, full |

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
| `tag` | `string` | yes | — | length ≥ 1 |
| `location` | `enum` |  | `"frontmatter"` | One of: `"frontmatter"`, `"inline"` |
| `prev_hash` | `string` |  | — | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `path` | `string` | yes | — |
| `tag` | `string` | yes | — |
| `location` | `enum` | yes | One of: `"frontmatter"`, `"inline"` |
| `added` | `boolean` | yes | — |
| `content_hash` | `string` | yes | — |
| `prev_hash` | `string` | yes | — |
| `conventions` | `object` |  | — |
| `conventions.warnings` | `object[]` |  | — |
| `conventions.warnings_omitted` | `integer` |  | range ≥ -9007199254740991 |
| `conventions.file_warnings` | `object[]` |  | — |
| `conventions.file_warnings_omitted` | `integer` |  | range ≥ -9007199254740991 |

## Related tools {#related-tools}

Other tools in the `metadata` domain: [`bulk_set_property`](/reliquary-tc/tools/reference/bulk_set_property/), [`find_notes_by_property`](/reliquary-tc/tools/reference/find_notes_by_property/), [`find_notes_by_tag`](/reliquary-tc/tools/reference/find_notes_by_tag/), [`get_conventions`](/reliquary-tc/tools/reference/get_conventions/), [`get_note_tags`](/reliquary-tc/tools/reference/get_note_tags/), [`list_properties`](/reliquary-tc/tools/reference/list_properties/), [`list_tags`](/reliquary-tc/tools/reference/list_tags/), [`read_frontmatter`](/reliquary-tc/tools/reference/read_frontmatter/), [`read_metadata_fields`](/reliquary-tc/tools/reference/read_metadata_fields/), [`read_property`](/reliquary-tc/tools/reference/read_property/), [`remove_tag`](/reliquary-tc/tools/reference/remove_tag/), [`suggest_tags`](/reliquary-tc/tools/reference/suggest_tags/), [`update_frontmatter`](/reliquary-tc/tools/reference/update_frontmatter/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
