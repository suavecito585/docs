---
title: "graph_path_between"
description: "Trace how one note connects to another through the persisted link graph: the shortest chain of notes joining them, with the edge types behind each hop."
editUrl: false
---

Trace how one note connects to another through the persisted link graph: the shortest chain of notes joining them, with the edge types behind each hop. Undirected by default, because a reader follows a backlink as readily as a link; directed:true answers the narrower 'can I reach B by following links out of A'. Returns connected:false when no chain exists within your read scope.

| | |
|---|---|
| **Domain** | links |
| **Scopes** | `read:notes` |
| **Access** | read |
| **Tags** | `read-only`, `domain:links`, `links`, `graph` |
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
| `from` | `string` | yes | — | length 1–1024 |
| `to` | `string` | yes | — | length 1–1024 |
| `directed` | `boolean` |  | `false` | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `vault` | `string` | yes | — |
| `from` | `string` | yes | — |
| `to` | `string` | yes | — |
| `directed` | `boolean` | yes | — |
| `connected` | `boolean` | yes | — |
| `from_in_graph` | `boolean` | yes | — |
| `to_in_graph` | `boolean` | yes | — |
| `hops` | `object[]` | yes | — |
| `hops[].from` | `string` | yes | — |
| `hops[].to` | `string` | yes | — |
| `hops[].via` | `string[]` | yes | — |
| `length` | `number \| null` | yes | — |

## Related tools {#related-tools}

Other tools in the `links` domain: [`find_link_cycles`](/reliquary-tc/tools/reference/find_link_cycles/), [`find_orphans`](/reliquary-tc/tools/reference/find_orphans/), [`find_unresolved_links`](/reliquary-tc/tools/reference/find_unresolved_links/), [`get_backlinks`](/reliquary-tc/tools/reference/get_backlinks/), [`get_link_strength`](/reliquary-tc/tools/reference/get_link_strength/), [`get_outgoing_links`](/reliquary-tc/tools/reference/get_outgoing_links/), [`graph_centrality`](/reliquary-tc/tools/reference/graph_centrality/), [`graph_communities`](/reliquary-tc/tools/reference/graph_communities/), [`prune_hub_links`](/reliquary-tc/tools/reference/prune_hub_links/), [`rewrite_link`](/reliquary-tc/tools/reference/rewrite_link/), [`suggest_links`](/reliquary-tc/tools/reference/suggest_links/), [`vault_health_score`](/reliquary-tc/tools/reference/vault_health_score/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
