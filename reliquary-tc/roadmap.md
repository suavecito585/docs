---
title: Roadmap
description: What has shipped through v2.0.1, and what remains deferred or out of scope.
---

The 2.x line is **Reliquary-TC**: the project was renamed in 2.0 and is licensed
under **Apache-2.0**. Releases through 1.34.x retain AGPL-3.0-only. The earlier
names keep working through 2.x; see the
[upgrade guide](https://github.com/The-40-Thieves/reliquary-tc/blob/main/docs/UPGRADING-2.0.md).

## Shipped (current: v2.0.1) {#shipped-current-v201}

The complete G2.1 tool surface — every tool across all domains — plus everything the
v1.x line added on top of the v1.0 hardening gate (OpenTelemetry, Prometheus,
CloudEvents, rate limiter, 8-triple native prebuilds, this docs site):

- **The measured retrieval engine** (v1.4–v1.7): enriched BM25 + enriched dense +
  hop-ordered wikilink expansion fused under RRF k=10 — a general hybrid retriever,
  gated by an n=250 golden set with a statistical ship rule (permutation test, FDR,
  a non-inferiority floor). Contextual chunk enrichment measured **+0.223 nDCG** and
  defaults on. k-means clustering and ACT-R activation recompute run as offline CLI
  passes. Per-vault GraphRAG edge isolation shipped. Mechanisms that did not earn a
  default ship **dark** behind flags. Cross-encoder rerankers and the class router have
  A/B results on the record (`docs/EVALUATION.md`, ADR 0007); learned sparse, ColBERT,
  convex fusion, query decomposition and MMR have **no recorded result**
  (`docs/DARK_MECHANISMS.md` is the inventory). **Graph densification** (derived `shared_tag` / vec0-kNN / LLM Pass-3 edges beyond authored wikilinks, `retrieval.densify.*`) is wired but **unmeasured** — it ships dark pending a multi-hop golden-set A/B (the earlier virtual-hop experiment hit an 80% bridge-recall ceiling; the champion figure it was compared against has since been [withdrawn as unreproducible](https://github.com/The-40-Thieves/reliquary-tc/pull/752), so that comparison needs re-deriving before it means anything).
- **The experiential work-memory tier** (v1.6): a quarantined second store with
  serve-path retrieval logging, auto-captured work episodes (poison-scanned,
  evaluator-stamped eligibility), and reader tools under a strict contract.
- **Composite context surfaces** (v1.7): `vault_context` (budget-packed one-call
  context with lesson surfacing and a TTL-enforced prewarm cache) and `reflect`
  (grounded synthesis + adversarial challenge + a typed-delta preference profile).
- **Dependency-aware deletion** with a hash-chained forget audit; **Obsidian Git**
  and **Remotely Save** companion bridges; a **knowledge-flywheel CLI family**
  (`metrics`, `gaps`, `prefetch`, `reflect`, `forget`, `citation-infer`,
  `contribution-report`, `activation-recompute`, `cluster`); and a vec0 index with
  a per-vault partition key, rebuilt in place from stored embeddings.
- **Local semantic search.** A fresh `reliquary-tc <vault>` selects the local
  embedder and supplies its cache directory. Docker, the `.mcpb` bundle and
  standalone binaries include it; npm users install
  `@the-40-thieves/reliquary-tc-embedder-local` separately. First use downloads and
  verifies pinned model weights, then inference runs locally without a separate
  embeddings service. A config file using the local provider must set `cacheDir`.
- **Remote access with OAuth.** The bundled authorization server ships authorize,
  token, refresh and revoke flows, passkey sign-in and RFC 8414 metadata. HTTP and
  the authorization server remain **opt-in**: enable `transports.http.enabled`
  and `auth.as.enabled`, with `auth.mode: jwt`, `auth.as.issuer` and `auth.resource`.
  Dynamic client registration is separately **opt-in** via
  `auth.as.dynamicRegistration`; the hardened profile forces it off.
- CycloneDX SBOMs, generated per package on release (`npm sbom`) and uploaded as
  build artifacts (non-blocking).

- **A reference page per tool**, generated from the live tool registry at docs build time
  (scopes, annotations, confirmation behaviour, parameter tables, output summary, related tools) and
  linked from the [tool catalog](/reliquary-tc/tools/tool-catalog/).

## Next {#next}

Themes under active work, in no particular order — see the tool reference and
configuration docs for what already ships today:

- **Zero-config semantic search.** The local backend now ships, but npm still
  needs the separate embedder install above. Semantic and graph-seeded retrieval
  with only a vault path is not yet universal across install paths.
- **Broader client coverage.** Verifying and documenting behavior across more MCP
  clients, beyond the ones already covered in the compatibility matrix.
- **Memory you own, in Markdown.** The experiential store already lives under the
  same ACL as the rest of the vault; ongoing work makes what it remembers, and why,
  more legible and more directly editable as plain notes.

## Deferred {#deferred}

- A per-scope HITL-raise (today per-scope overrides only tighten; isolate unattended
  automation on a second instance instead).

## Out of scope for the current line {#out-of-scope-for-the-current-line}

- The **typed-atom MemIR substrate** (claim atoms, bi-temporal
  `authoritative_claims`) — a downstream engine-build phase, parked with an explicit
  revisit trigger.
- **Cross-store fused ranking** between the authored vault and the experiential
  store — the stores federate at query time by design (separate legs, never one
  ranked list), so score calibration across them has no substrate (this was
  investigated and closed with that verdict).
