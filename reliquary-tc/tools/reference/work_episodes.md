---
title: "work_episodes"
description: "List/inspect the raw experiential episode log (management surface, the first-party list/inspect verb)."
editUrl: false
---

List/inspect the raw experiential episode log (management surface, the first-party list/inspect verb). Shows pending and ineligible state for review; tombstoned rows stay hidden unless include_blocked. Partitioned to the calling principal unless any_caller, which requires the admin:workspace scope (P1.7). Set unstamped_debt to see judgeable work that still carries no verdict — yours, or every principal's when combined with any_caller — pair it with `until` to mean 'older than' — then clear it with work_result. Protocol traffic and the verdict verbs themselves never appear there; they are not work anyone can judge. response_format=concise returns each episode without vault, caller, channel, episode_type, duration_ms, result_size and null or empty fields; trust, eligibility, session_id and a true blocked flag are kept.

| | |
|---|---|
| **Domain** | knowledge |
| **Scopes** | `read:workspace` |
| **Access** | read |
| **Tags** | `read-only`, `domain:knowledge`, `experiential` |
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
| `session_id` | `string` |  | — | — |
| `tool` | `string` |  | — | — |
| `status` | `enum` |  | — | One of: `"ok"`, `"error"`, `"skipped"` |
| `since` | `integer` |  | — | range ≥ 1 |
| `until` | `integer` |  | — | range ≥ 1 |
| `include_blocked` | `boolean` |  | `false` | — |
| `any_caller` | `boolean` |  | `false` | — |
| `unstamped_debt` | `boolean` |  | `false` | — |
| `k` | `integer` |  | `50` | range 1–500 |
| `response_format` | `enum` |  | — | concise returns only the high-signal fields; detailed (the shipped default) returns the full payload. Errors and safety warnings are never trimmed. When omitted, the server's tools.defaults.responseFormat applies. One of: `"concise"`, `"detailed"` |
| `verbosity` | `enum` |  | — | Legacy alias for response_format: terse = concise, full = detailed. One of: `"full"`, `"terse"` |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `available` | `boolean` | yes | — |
| `message` | `string` |  | — |
| `episodes` | `object[]` |  | — |
| `episodes[].id` | `string` | with parent | — |
| `episodes[].ts` | `number` | with parent | — |
| `episodes[].vault` | `string \| null` |  | — |
| `episodes[].session_id` | `string \| null` |  | — |
| `episodes[].caller` | `string \| null` |  | — |
| `episodes[].channel` | `string` |  | — |
| `episodes[].episode_type` | `string` |  | — |
| `episodes[].task_result` | `number \| null` |  | — |
| `episodes[].verdict_at` | `number \| null` |  | — |
| `episodes[].tool` | `string \| null` |  | — |
| `episodes[].status` | `string` | with parent | — |
| `episodes[].error_code` | `string \| null` |  | — |
| `episodes[].duration_ms` | `number \| null` |  | — |
| `episodes[].result_size` | `number \| null` |  | — |
| `episodes[].summary` | `string \| null` |  | — |
| `episodes[].tags` | `string[]` |  | — |
| `episodes[].trust` | `number \| null` |  | — |
| `episodes[].eligibility` | `string` | with parent | — |
| `episodes[].blocked` | `boolean` |  | — |
| `episodes[].prev_id` | `string \| null` |  | — |

## Related tools {#related-tools}

Other tools in the `knowledge` domain: [`add_observation`](/reliquary-tc/tools/reference/add_observation/), [`audit_provenance`](/reliquary-tc/tools/reference/audit_provenance/), [`close_goal`](/reliquary-tc/tools/reference/close_goal/), [`commit_capture`](/reliquary-tc/tools/reference/commit_capture/), [`commit_wiki_page`](/reliquary-tc/tools/reference/commit_wiki_page/), [`create_entity`](/reliquary-tc/tools/reference/create_entity/), [`delete_entity`](/reliquary-tc/tools/reference/delete_entity/), [`diagnose_retrieval`](/reliquary-tc/tools/reference/diagnose_retrieval/), [`draft_wiki_page`](/reliquary-tc/tools/reference/draft_wiki_page/), [`end_session`](/reliquary-tc/tools/reference/end_session/), [`enqueue_capture`](/reliquary-tc/tools/reference/enqueue_capture/), [`episode_stats`](/reliquary-tc/tools/reference/episode_stats/), [`explain_answer`](/reliquary-tc/tools/reference/explain_answer/), [`find_existing_page`](/reliquary-tc/tools/reference/find_existing_page/), [`gap_report`](/reliquary-tc/tools/reference/gap_report/), [`get_entity`](/reliquary-tc/tools/reference/get_entity/), [`get_session_traces`](/reliquary-tc/tools/reference/get_session_traces/), [`knowledge_challenge`](/reliquary-tc/tools/reference/knowledge_challenge/), [`link_entities`](/reliquary-tc/tools/reference/link_entities/), [`lint_wiki`](/reliquary-tc/tools/reference/lint_wiki/), [`list_capture_queue`](/reliquary-tc/tools/reference/list_capture_queue/), [`list_contradictions`](/reliquary-tc/tools/reference/list_contradictions/), [`list_goals`](/reliquary-tc/tools/reference/list_goals/), [`note_quality_report`](/reliquary-tc/tools/reference/note_quality_report/), [`plur_get`](/reliquary-tc/tools/reference/plur_get/), [`plur_recall`](/reliquary-tc/tools/reference/plur_recall/), [`plur_recall_hybrid`](/reliquary-tc/tools/reference/plur_recall_hybrid/), [`plur_similarity_search`](/reliquary-tc/tools/reference/plur_similarity_search/), [`query_entity_graph`](/reliquary-tc/tools/reference/query_entity_graph/), [`record_retrieval_feedback`](/reliquary-tc/tools/reference/record_retrieval_feedback/), [`reflect`](/reliquary-tc/tools/reference/reflect/), [`rename_entity`](/reliquary-tc/tools/reference/rename_entity/), [`session_bootstrap`](/reliquary-tc/tools/reference/session_bootstrap/), [`set_goal`](/reliquary-tc/tools/reference/set_goal/), [`start_session`](/reliquary-tc/tools/reference/start_session/), [`unlink_entities`](/reliquary-tc/tools/reference/unlink_entities/), [`update_observation`](/reliquary-tc/tools/reference/update_observation/), [`vault_context`](/reliquary-tc/tools/reference/vault_context/), [`vault_graph_search`](/reliquary-tc/tools/reference/vault_graph_search/), [`work_episode_chain`](/reliquary-tc/tools/reference/work_episode_chain/), [`work_forget`](/reliquary-tc/tools/reference/work_forget/), [`work_result`](/reliquary-tc/tools/reference/work_result/), [`work_search`](/reliquary-tc/tools/reference/work_search/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
