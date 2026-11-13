---
title: "suggest_links"
description: "Suggest notes to link a given note to, from the link graph (co-citation with the note's inbound sources + 2-hop outbound neighbors), excluding notes it already links to."
editUrl: false
---

Suggest notes to link a given note to, from the link graph (co-citation with the note's inbound sources + 2-hop outbound neighbors), excluding notes it already links to. Graph-based (no embeddings). response_format=concise returns \{path, score\} per suggestion without the score components, the path echo and total.

| | |
|---|---|
| **Domain** | links |
| **Scopes** | `read:notes` |
| **Access** | read |
| **Tags** | `read-only`, `domain:links` |
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
| `limit` | `integer` |  | `20` | range 1–200 |
| `response_format` | `enum` |  | — | concise returns only the high-signal fields; detailed (the shipped default) returns the full payload. Errors and safety warnings are never trimmed. When omitted, the server's tools.defaults.responseFormat applies. One of: `"concise"`, `"detailed"` |
| `verbosity` | `enum` |  | — | Legacy alias for response_format: terse = concise, full = detailed. One of: `"full"`, `"terse"` |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `warnings` | `object[]` |  | — |
| `warnings[].path` | `string` | with parent | — |
| `warnings[].reason` | `enum` | with parent | One of: `"frontmatter_yaml"` |
| `warnings[].message` | `string` | with parent | — |
| `warnings_omitted` | `integer` |  | range ≥ -9007199254740991 |
| `notes_read_refused` | `integer` |  | range ≥ -9007199254740991 |
| `vault` | `string` | yes | — |
| `path` | `string` |  | — |
| `total` | `number` |  | — |
| `suggestions` | `object[]` | yes | — |
| `suggestions[].path` | `string` | yes | — |
| `suggestions[].score` | `number` | yes | — |
| `suggestions[].co_citation` | `number` |  | — |
| `suggestions[].two_hop` | `number` |  | — |

## Related tools {#related-tools}

Other tools in the `links` domain: [`find_link_cycles`](/reliquary-tc/tools/reference/find_link_cycles/), [`find_orphans`](/reliquary-tc/tools/reference/find_orphans/), [`find_unresolved_links`](/reliquary-tc/tools/reference/find_unresolved_links/), [`get_backlinks`](/reliquary-tc/tools/reference/get_backlinks/), [`get_link_strength`](/reliquary-tc/tools/reference/get_link_strength/), [`get_outgoing_links`](/reliquary-tc/tools/reference/get_outgoing_links/), [`graph_centrality`](/reliquary-tc/tools/reference/graph_centrality/), [`graph_communities`](/reliquary-tc/tools/reference/graph_communities/), [`graph_path_between`](/reliquary-tc/tools/reference/graph_path_between/), [`prune_hub_links`](/reliquary-tc/tools/reference/prune_hub_links/), [`rewrite_link`](/reliquary-tc/tools/reference/rewrite_link/), [`vault_health_score`](/reliquary-tc/tools/reference/vault_health_score/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
