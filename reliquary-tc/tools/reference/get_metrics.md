---
title: "get_metrics"
description: "Snapshot Prometheus-style metrics as structured JSON: per-(vault,tool,status) invocation counters and rate-limit-hit counters aggregated from the local event_log + live limiter, plus uptime/registe..."
editUrl: false
---

Snapshot Prometheus-style metrics as structured JSON: per-(vault,tool,status) invocation counters and rate-limit-hit counters aggregated from the local event_log + live limiter, plus uptime/registered-vault/registered-tool gauges. Optionally filter to one vault. Domain: admin.

| | |
|---|---|
| **Domain** | admin |
| **Scopes** | `admin:metrics` |
| **Access** | write |
| **Tags** | `read-only`, `admin`, `domain:admin` |
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
| `vault` | `string` |  | — | length 1–64; pattern `^[a-z0-9_-]+$` |

## Output {#output}

| Field | Type | Always present | Description |
|---|---|---|---|
| `metrics` | `object[]` | yes | — |
| `metrics[].name` | `string` | yes | — |
| `metrics[].type` | `enum` | yes | One of: `"counter"`, `"gauge"` |
| `metrics[].value` | `number` | yes | — |
| `metrics[].labels` | `Record<string, string>` | yes | — |

## Related tools {#related-tools}

Other tools in the `admin` domain: [`cancel_task`](/reliquary-tc/tools/reference/cancel_task/), [`get_index_status`](/reliquary-tc/tools/reference/get_index_status/), [`get_server_config`](/reliquary-tc/tools/reference/get_server_config/), [`get_task_status`](/reliquary-tc/tools/reference/get_task_status/), [`inspect_acl`](/reliquary-tc/tools/reference/inspect_acl/), [`inspect_visibility`](/reliquary-tc/tools/reference/inspect_visibility/), [`server_health`](/reliquary-tc/tools/reference/server_health/), [`session_rerun`](/reliquary-tc/tools/reference/session_rerun/).

Back to the [tool catalog](/reliquary-tc/tools/tool-catalog/).
