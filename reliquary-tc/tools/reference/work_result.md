---
title: "work_result"
description: "Record how the task you just finished went, as -1 (it failed or produced a bad result), 0 (neutral) or +1 (it worked)."
editUrl: false
---

Record how the task you just finished went, as -1 (it failed or produced a bad result), 0 (neutral) or +1 (it worked). The verdict applies to every judgeable tool call in your current session that has no verdict yet, and then a fresh window opens — so calling this once at the end of a session covers the session, and calling it after each task partitions the session into those tasks. Protocol traffic and this verb itself are never judged. Nothing else writes agent_episodes.task_result, and two retrieval behaviours read it: a -1 holds those episodes out of promotion, and the preference extractor only ever learns from episodes carrying a verdict.

| | |
|---|---|
| **Domain** | knowledge |
| **Scopes** | `write:workspace` |
| **Access** | write |
| **Tags** | `writes`, `domain:knowledge`, `experiential`, `verdict` |
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
| `result` | `number` | yes | — | -1 bad, 0 neutral, +1 good. Allowed values: -1, 0, 1. range -1–1 |
| `as_of` | `integer` |  | — | Epoch ms ceiling: only calls at or before this are judged. Defaults to now. Use it when work continued while you were deciding — the server cannot observe your task boundary and will otherwise sweep in anything committed before this call landed. range ≥ 1 |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `available` | `boolean` | yes | — |
| `message` | `string` |  | — |
| `stamped` | `number` |  | — |
| `demoted` | `number` |  | — |
| `session_id` | `string` |  | — |
| `verdict_at` | `number` |  | — |

## Related tools {#related-tools}

Other tools in the `knowledge` domain: [`add_observation`](/reliquary-tc/tools/reference/add_observation/), [`audit_provenance`](/reliquary-tc/tools/reference/audit_provenance/), [`close_goal`](/reliquary-tc/tools/reference/close_goal/), [`commit_capture`](/reliquary-tc/tools/reference/commit_capture/), [`commit_wiki_page`](/reliquary-tc/tools/reference/commit_wiki_page/), [`create_entity`](/reliquary-tc/tools/reference/create_entity/), [`delete_entity`](/reliquary-tc/tools/reference/delete_entity/), [`diagnose_retrieval`](/reliquary-tc/tools/reference/diagnose_retrieval/), [`draft_wiki_page`](/reliquary-tc/tools/reference/draft_wiki_page/), [`end_session`](/reliquary-tc/tools/reference/end_session/), [`enqueue_capture`](/reliquary-tc/tools/reference/enqueue_capture/), [`episode_stats`](/reliquary-tc/tools/reference/episode_stats/), [`explain_answer`](/reliquary-tc/tools/reference/explain_answer/), [`find_existing_page`](/reliquary-tc/tools/reference/find_existing_page/), [`gap_report`](/reliquary-tc/tools/reference/gap_report/), [`get_entity`](/reliquary-tc/tools/reference/get_entity/), [`get_session_traces`](/reliquary-tc/tools/reference/get_session_traces/), [`knowledge_challenge`](/reliquary-tc/tools/reference/knowledge_challenge/), [`link_entities`](/reliquary-tc/tools/reference/link_entities/), [`lint_wiki`](/reliquary-tc/tools/reference/lint_wiki/), [`list_capture_queue`](/reliquary-tc/tools/reference/list_capture_queue/), [`list_contradictions`](/reliquary-tc/tools/reference/list_contradictions/), [`list_goals`](/reliquary-tc/tools/reference/list_goals/), [`note_quality_report`](/reliquary-tc/tools/reference/note_quality_report/), [`plur_get`](/reliquary-tc/tools/reference/plur_get/), [`plur_recall`](/reliquary-tc/tools/reference/plur_recall/), [`plur_recall_hybrid`](/reliquary-tc/tools/reference/plur_recall_hybrid/), [`plur_similarity_search`](/reliquary-tc/tools/reference/plur_similarity_search/), [`query_entity_graph`](/reliquary-tc/tools/reference/query_entity_graph/), [`record_retrieval_feedback`](/reliquary-tc/tools/reference/record_retrieval_feedback/), [`reflect`](/reliquary-tc/tools/reference/reflect/), [`rename_entity`](/reliquary-tc/tools/reference/rename_entity/), [`session_bootstrap`](/reliquary-tc/tools/reference/session_bootstrap/), [`set_goal`](/reliquary-tc/tools/reference/set_goal/), [`start_session`](/reliquary-tc/tools/reference/start_session/), [`unlink_entities`](/reliquary-tc/tools/reference/unlink_entities/), [`update_observation`](/reliquary-tc/tools/reference/update_observation/), [`vault_context`](/reliquary-tc/tools/reference/vault_context/), [`vault_graph_search`](/reliquary-tc/tools/reference/vault_graph_search/), [`work_episode_chain`](/reliquary-tc/tools/reference/work_episode_chain/), [`work_episodes`](/reliquary-tc/tools/reference/work_episodes/), [`work_forget`](/reliquary-tc/tools/reference/work_forget/), [`work_search`](/reliquary-tc/tools/reference/work_search/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
