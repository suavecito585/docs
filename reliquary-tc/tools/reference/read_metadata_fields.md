---
title: "read_metadata_fields"
description: "Read a note's typed metadata fields via the Metadata Menu plugin: returns each configured field's name, value, type, validity, and source (frontmatter vs inline)."
editUrl: false
---

Read a note's typed metadata fields via the Metadata Menu plugin: returns each configured field's name, value, type, validity, and source (frontmatter vs inline). Read-only field introspection.

| | |
|---|---|
| **Domain** | metadata |
| **Scopes** | `read:metadata-menu` |
| **Access** | read |
| **Tags** | `read-only`, `plugin-bridge`, `domain:metadata` |
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
| `path` | `string` | yes | — | length 1–1024 |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `path` | `string` | yes | — |
| `fields` | `Record<string, any>` | yes | — |
| `total` | `integer` | yes | range ≥ 0 |
| `vault` | `string` | yes | — |

## Related tools {#related-tools}

Other tools in the `metadata` domain: [`add_tag`](/reliquary-tc/tools/reference/add_tag/), [`bulk_set_property`](/reliquary-tc/tools/reference/bulk_set_property/), [`find_notes_by_property`](/reliquary-tc/tools/reference/find_notes_by_property/), [`find_notes_by_tag`](/reliquary-tc/tools/reference/find_notes_by_tag/), [`get_conventions`](/reliquary-tc/tools/reference/get_conventions/), [`get_note_tags`](/reliquary-tc/tools/reference/get_note_tags/), [`list_properties`](/reliquary-tc/tools/reference/list_properties/), [`list_tags`](/reliquary-tc/tools/reference/list_tags/), [`read_frontmatter`](/reliquary-tc/tools/reference/read_frontmatter/), [`read_property`](/reliquary-tc/tools/reference/read_property/), [`remove_tag`](/reliquary-tc/tools/reference/remove_tag/), [`suggest_tags`](/reliquary-tc/tools/reference/suggest_tags/), [`update_frontmatter`](/reliquary-tc/tools/reference/update_frontmatter/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
