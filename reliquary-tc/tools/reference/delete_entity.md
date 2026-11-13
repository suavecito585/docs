---
title: "delete_entity"
description: "Delete a memory entity outright — the escape hatch for 'created it by accident', NOT the primary retirement path (use rename_entity's status param to retire instead; that stays reversible, this doe..."
editUrl: false
---

Delete a memory entity outright — the escape hatch for 'created it by accident', NOT the primary retirement path (use rename_entity's status param to retire instead; that stays reversible, this doesn't). Destructive; requires confirmation. Dependency-aware like `forget`: refuses when the entity has any relation, incoming or outgoing, unless cascade is set — in which case those relations are removed too and every OTHER materialized entity that referenced this one has its note re-materialized so its `[[links]]` stop dangling. The entity's own note is trashed (recoverable) unless permanent is set.

| | |
|---|---|
| **Domain** | knowledge |
| **Scopes** | `delete:memory` |
| **Access** | destructive |
| **Tags** | `writes`, `destructive`, `hitl`, `domain:knowledge` |
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

- The confirmation binds to a fingerprint of the state being approved, so a confirmation given for since-changed state is refused with `replay_drift`.

## Input {#input}

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `vault` | `string` |  | — | Vault id. May be omitted when only one vault is available. length 1–64; pattern `^[a-z0-9_-]+$` |
| `entity_id` | `string` | yes | — | length ≥ 1 |
| `cascade` | `boolean` |  | `false` | — |
| `permanent` | `boolean` |  | `false` | — |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `entity_id` | `string` | yes | — |
| `deleted` | `boolean` | yes | — |
| `relations_deleted` | `number` | yes | — |
| `vault_path` | `string \| null` | yes | — |
| `permanent` | `boolean` | yes | — |
| `trashed_to` | `string \| null` | yes | — |

## Related tools {#related-tools}

Other tools in the `knowledge` domain: [`add_observation`](/reliquary-tc/tools/reference/add_observation/), [`audit_provenance`](/reliquary-tc/tools/reference/audit_provenance/), [`close_goal`](/reliquary-tc/tools/reference/close_goal/), [`commit_capture`](/reliquary-tc/tools/reference/commit_capture/), [`commit_wiki_page`](/reliquary-tc/tools/reference/commit_wiki_page/), [`create_entity`](/reliquary-tc/tools/reference/create_entity/), [`diagnose_retrieval`](/reliquary-tc/tools/reference/diagnose_retrieval/), [`draft_wiki_page`](/reliquary-tc/tools/reference/draft_wiki_page/), [`end_session`](/reliquary-tc/tools/reference/end_session/), [`enqueue_capture`](/reliquary-tc/tools/reference/enqueue_capture/), [`episode_stats`](/reliquary-tc/tools/reference/episode_stats/), [`explain_answer`](/reliquary-tc/tools/reference/explain_answer/), [`find_existing_page`](/reliquary-tc/tools/reference/find_existing_page/), [`gap_report`](/reliquary-tc/tools/reference/gap_report/), [`get_entity`](/reliquary-tc/tools/reference/get_entity/), [`get_session_traces`](/reliquary-tc/tools/reference/get_session_traces/), [`knowledge_challenge`](/reliquary-tc/tools/reference/knowledge_challenge/), [`link_entities`](/reliquary-tc/tools/reference/link_entities/), [`lint_wiki`](/reliquary-tc/tools/reference/lint_wiki/), [`list_capture_queue`](/reliquary-tc/tools/reference/list_capture_queue/), [`list_contradictions`](/reliquary-tc/tools/reference/list_contradictions/), [`list_goals`](/reliquary-tc/tools/reference/list_goals/), [`note_quality_report`](/reliquary-tc/tools/reference/note_quality_report/), [`plur_get`](/reliquary-tc/tools/reference/plur_get/), [`plur_recall`](/reliquary-tc/tools/reference/plur_recall/), [`plur_recall_hybrid`](/reliquary-tc/tools/reference/plur_recall_hybrid/), [`plur_similarity_search`](/reliquary-tc/tools/reference/plur_similarity_search/), [`query_entity_graph`](/reliquary-tc/tools/reference/query_entity_graph/), [`record_retrieval_feedback`](/reliquary-tc/tools/reference/record_retrieval_feedback/), [`reflect`](/reliquary-tc/tools/reference/reflect/), [`rename_entity`](/reliquary-tc/tools/reference/rename_entity/), [`session_bootstrap`](/reliquary-tc/tools/reference/session_bootstrap/), [`set_goal`](/reliquary-tc/tools/reference/set_goal/), [`start_session`](/reliquary-tc/tools/reference/start_session/), [`unlink_entities`](/reliquary-tc/tools/reference/unlink_entities/), [`update_observation`](/reliquary-tc/tools/reference/update_observation/), [`vault_context`](/reliquary-tc/tools/reference/vault_context/), [`vault_graph_search`](/reliquary-tc/tools/reference/vault_graph_search/), [`work_episode_chain`](/reliquary-tc/tools/reference/work_episode_chain/), [`work_episodes`](/reliquary-tc/tools/reference/work_episodes/), [`work_forget`](/reliquary-tc/tools/reference/work_forget/), [`work_result`](/reliquary-tc/tools/reference/work_result/), [`work_search`](/reliquary-tc/tools/reference/work_search/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
