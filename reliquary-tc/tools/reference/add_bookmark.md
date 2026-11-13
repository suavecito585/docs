---
title: "add_bookmark"
description: "Add a bookmark (optionally into a named group, created if absent)."
editUrl: false
---

Add a bookmark (optionally into a named group, created if absent). A duplicate is a no-op unless allow_duplicate is set. Domain: workspace.

| | |
|---|---|
| **Domain** | workspace |
| **Scopes** | `write:bookmarks` |
| **Access** | write |
| **Tags** | `writes`, `domain:workspace` |
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
| `bookmark` | `object` | yes | — | — |
| `bookmark.type` | `enum` | yes | — | One of: `"file"`, `"folder"`, `"search"`, `"graph"`, `"url"`, `"group"`, `"heading"`, `"block"` |
| `bookmark.path` | `string` |  | — | — |
| `bookmark.subpath` | `string` |  | — | — |
| `bookmark.url` | `string` |  | — | — |
| `bookmark.query` | `string` |  | — | — |
| `bookmark.title` | `string` |  | — | — |
| `group` | `string` |  | — | length ≥ 1 |
| `allow_duplicate` | `boolean` |  | `false` | — |
| `prev_hash` | `string` |  | — | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `added` | `boolean` | yes | — |
| `duplicate` | `boolean` | yes | — |
| `group` | `string \| null` | yes | — |
| `count` | `integer` | yes | range ≥ -9007199254740991 |
| `content_hash` | `string` | yes | — |

## Related tools {#related-tools}

Other tools in the `workspace` domain: [`append_active_file`](/reliquary-tc/tools/reference/append_active_file/), [`append_to_periodic_note`](/reliquary-tc/tools/reference/append_to_periodic_note/), [`create_periodic_note`](/reliquary-tc/tools/reference/create_periodic_note/), [`delete_active_file`](/reliquary-tc/tools/reference/delete_active_file/), [`find_or_create_periodic_note`](/reliquary-tc/tools/reference/find_or_create_periodic_note/), [`get_active_file`](/reliquary-tc/tools/reference/get_active_file/), [`get_periodic_note`](/reliquary-tc/tools/reference/get_periodic_note/), [`list_bookmarks`](/reliquary-tc/tools/reference/list_bookmarks/), [`list_periodic_notes`](/reliquary-tc/tools/reference/list_periodic_notes/), [`list_workspaces`](/reliquary-tc/tools/reference/list_workspaces/), [`open_workspace`](/reliquary-tc/tools/reference/open_workspace/), [`patch_active_file`](/reliquary-tc/tools/reference/patch_active_file/), [`remove_bookmark`](/reliquary-tc/tools/reference/remove_bookmark/), [`resolve_daily_note`](/reliquary-tc/tools/reference/resolve_daily_note/), [`save_workspace`](/reliquary-tc/tools/reference/save_workspace/), [`update_active_file`](/reliquary-tc/tools/reference/update_active_file/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
