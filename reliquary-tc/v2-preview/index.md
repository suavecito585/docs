---
title: V2 Preview
description: Earlier substrate proposals, distinct from the released 2.x line.
---

The 2.x line has shipped: the project was renamed to Reliquary-TC in 2.0, under
Apache-2.0, with v2.0.1 the first published release. The "V2" in this page's
title refers to a next substrate generation, not the released 2.x line.

The v1.x line went further than this page originally scoped: the 2026-07 retrieval
campaign shipped the general BM25 + dense hybrid retriever (enriched lexical +
enriched dense + hop-ordered graph expansion under RRF), k-means clustering and
ACT-R activation as offline CLI passes, and the v1.6–v1.7 memory engine (the
experiential work-memory tier, composite context surfaces, dependency-aware
deletion, the knowledge flywheel). See the [Roadmap](/reliquary-tc/roadmap/) for the shipped
list.

The earlier substrate proposals remain outside the current line:

- **The typed-atom MemIR substrate** — claim atoms, bi-temporal
  `authoritative_claims`, `derives_from` provenance edges. Parked with an explicit
  revisit trigger: it lands with a purpose-built claim-extraction
  pipeline, and pulls reference-counted derived-artifact GC (upgrading `forget`'s
  cascade) with it.
- **An episode → authored-claim promotion path** — deliberately absent today (the
  experiential store is a membrane; injected episodes structurally cannot reach
  authored atoms). If a future substrate adds promotion, the pre-recorded safety
  precondition applies: full dependency-closure deletion becomes a write-on gate.
- **Cross-store fused ranking** — the authored vault and the experiential store
  federate at query time as separate legs by design. A single fused ranking (and
  the PIT score calibration it would need) remains a substrate question, taken up
  only with a concrete proposal.

Dark v1.x mechanisms are not substrate items either, and they are not equally
available. Rerankers and the query class router ship behind config flags, off by
default. Learned sparse and ColBERT are wired but need a multi-vector encoder
that a default install does not provide. Convex fusion and query decomposition
are reachable only from the evaluation harness. `docs/DARK_MECHANISMS.md` is the
inventory, with each mechanism's recorded result; any of them re-enters when a
larger eval set or better serving stack changes its measured verdict.

These are previews of direction, not commitments of schedule or a release number.
See the [Roadmap](/reliquary-tc/roadmap/) for what ships and what remains deferred.
