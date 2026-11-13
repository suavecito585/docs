---
title: "audit_provenance"
description: "Provenance audit: flag claim-bearing notes that lack a 'sources' frontmatter field and cite nothing in the body."
editUrl: false
---

Provenance audit: flag claim-bearing notes that lack a 'sources' frontmatter field and cite nothing in the body. A note with no sources field but a URL, a footnote definition or a Sources/References section with a list or link is reported as cited in body only (body_only), not missing. Reports coverage of sources/confidence/verified across the readable note set. Read-only. Excludes daily notes, templates, and index files by default; tune scope with include/exclude globs, the field name, and types (only notes whose frontmatter type matches are claim-bearing; the rest are counted in skipped_by_type). response_format=concise drops the field echo, with_provenance and the by_folder breakdown.

| | |
|---|---|
| **Domain** | knowledge |
| **Scopes** | `read:notes` |
| **Access** | read |
| **Tags** | `read-only`, `domain:knowledge` |
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
| `field` | `string` |  | `"sources"` | length ≥ 1 |
| `include` | `string[]` |  | — | items ≤ 64 |
| `exclude` | `string[]` |  | — | items ≤ 64 |
| `types` | `string[]` |  | — | items 1–64 |
| `limit` | `integer` |  | `100` | range 1–2000 |
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
| `field` | `string` |  | — |
| `scanned` | `number` | yes | — |
| `with_provenance` | `number` |  | — |
| `missing_provenance` | `number` | yes | — |
| `coverage` | `number` | yes | — |
| `confidence_coverage` | `number` | yes | — |
| `verified_coverage` | `number` | yes | — |
| `by_folder` | `Record<string, object>` |  | — |
| `missing` | `string[]` | yes | — |
| `body_only` | `object[]` | yes | — |
| `body_only[].path` | `string` | yes | — |
| `body_only[].evidence` | `enum[]` | yes | — |
| `body_only_count` | `number` | yes | — |
| `skipped_by_type` | `number` | yes | — |
| `truncated` | `boolean` | yes | — |

## Related tools {#related-tools}

Other tools in the `knowledge` domain: [`add_observation`](/reliquary-tc/tools/reference/add_observation/), [`close_goal`](/reliquary-tc/tools/reference/close_goal/), [`commit_capture`](/reliquary-tc/tools/reference/commit_capture/), [`commit_wiki_page`](/reliquary-tc/tools/reference/commit_wiki_page/), [`create_entity`](/reliquary-tc/tools/reference/create_entity/), [`delete_entity`](/reliquary-tc/tools/reference/delete_entity/), [`diagnose_retrieval`](/reliquary-tc/tools/reference/diagnose_retrieval/), [`draft_wiki_page`](/reliquary-tc/tools/reference/draft_wiki_page/), [`end_session`](/reliquary-tc/tools/reference/end_session/), [`enqueue_capture`](/reliquary-tc/tools/reference/enqueue_capture/), [`episode_stats`](/reliquary-tc/tools/reference/episode_stats/), [`explain_answer`](/reliquary-tc/tools/reference/explain_answer/), [`find_existing_page`](/reliquary-tc/tools/reference/find_existing_page/), [`gap_report`](/reliquary-tc/tools/reference/gap_report/), [`get_entity`](/reliquary-tc/tools/reference/get_entity/), [`get_session_traces`](/reliquary-tc/tools/reference/get_session_traces/), [`knowledge_challenge`](/reliquary-tc/tools/reference/knowledge_challenge/), [`link_entities`](/reliquary-tc/tools/reference/link_entities/), [`lint_wiki`](/reliquary-tc/tools/reference/lint_wiki/), [`list_capture_queue`](/reliquary-tc/tools/reference/list_capture_queue/), [`list_contradictions`](/reliquary-tc/tools/reference/list_contradictions/), [`list_goals`](/reliquary-tc/tools/reference/list_goals/), [`note_quality_report`](/reliquary-tc/tools/reference/note_quality_report/), [`plur_get`](/reliquary-tc/tools/reference/plur_get/), [`plur_recall`](/reliquary-tc/tools/reference/plur_recall/), [`plur_recall_hybrid`](/reliquary-tc/tools/reference/plur_recall_hybrid/), [`plur_similarity_search`](/reliquary-tc/tools/reference/plur_similarity_search/), [`query_entity_graph`](/reliquary-tc/tools/reference/query_entity_graph/), [`record_retrieval_feedback`](/reliquary-tc/tools/reference/record_retrieval_feedback/), [`reflect`](/reliquary-tc/tools/reference/reflect/), [`rename_entity`](/reliquary-tc/tools/reference/rename_entity/), [`session_bootstrap`](/reliquary-tc/tools/reference/session_bootstrap/), [`set_goal`](/reliquary-tc/tools/reference/set_goal/), [`start_session`](/reliquary-tc/tools/reference/start_session/), [`unlink_entities`](/reliquary-tc/tools/reference/unlink_entities/), [`update_observation`](/reliquary-tc/tools/reference/update_observation/), [`vault_context`](/reliquary-tc/tools/reference/vault_context/), [`vault_graph_search`](/reliquary-tc/tools/reference/vault_graph_search/), [`work_episode_chain`](/reliquary-tc/tools/reference/work_episode_chain/), [`work_episodes`](/reliquary-tc/tools/reference/work_episodes/), [`work_forget`](/reliquary-tc/tools/reference/work_forget/), [`work_result`](/reliquary-tc/tools/reference/work_result/), [`work_search`](/reliquary-tc/tools/reference/work_search/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
