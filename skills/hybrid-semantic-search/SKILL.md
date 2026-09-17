---
name: hybrid-semantic-search
description: Design, implement, or review local hybrid search that combines metadata or SQL filtering with embedding similarity, persistent vector artifacts, stable record mapping, and reproducible ranking. Use for semantic retrieval over structured datasets, not for autonomous agents or generative-answer systems.
---

# Hybrid Semantic Search

Create retrieval that preserves the structured dataset as the system of record
and uses embeddings only for semantic ranking.

## Recommend the production target first

Treat stated requirements and the current sample corpus as minimum
acceptance criteria, not as the architecture ceiling. When the user wants a
real-world solution, recommend the storage, indexing, serving, and publication
design suited to credible production corpus size, query concurrency, update
frequency, latency, and recovery needs. Do not choose an unindexed scan or a
local NumPy artifact solely because the sample dataset is small.

Distinguish the production recommendation from local execution. A local
machine may use a compatible single-node implementation, emulator, or bounded
test path when the production system cannot run locally, but present that as a
development constraint rather than the preferred architecture. Make any
temporary compromise explicit and identify its scaling limit or migration
trigger.

## Establish the retrieval contract

Identify the searchable record grain, text fields, stable record identifier,
filterable metadata, embedding model, ranking metric, and expected behavior for
empty or invalid queries. Keep filtering semantics independent from vector
ranking semantics.

## Build persistent embeddings

- Construct input text deterministically from documented fields.
- Persist the embedding model name, dimensions, stable record identity, and
  vector values in one authoritative vector store.
- Validate that record IDs and stored vectors have identical cardinality and
  deterministic mapping when loading or publishing.
- Normalize stored vectors and query vectors when using dot product as cosine
  similarity.
- Exclude the query record itself when computing neighbors for a stored row.
- Version or rebuild artifacts when the model or text construction changes.
- Treat the embedding table, vector index, model metadata, and any precomputed
  neighbor export as one publication contract. Expose stale state when they
  cannot be promoted atomically.
- After incremental records arrive, recompute neighbor lists whose candidate
  set is the full corpus; a new vector can change an existing record's top-k.

Use a local vector implementation only as an execution-compatible form of the
target design. For production recommendations, choose indexed storage and a
serving architecture from projected corpus size, update frequency,
concurrency, latency, durability, and filtered-search requirements.

## Combine structured and semantic retrieval

Apply deterministic metadata or SQL filters first, then rank the eligible
record IDs by similarity. Preserve the stable ID mapping across structured
records, embeddings, and the vector index. Return enough metadata for a caller
to trace each result to its source record.

Never treat semantic similarity as factual verification or silently broaden a
filter because too few results remain.

## Verify

Test matrix round-tripping, ID alignment, normalization, self-exclusion,
top-k bounds, deterministic tie handling, filter correctness, and behavior when
no records qualify. Use tiny synthetic vectors for unit tests so correctness
does not depend on downloading a model.

## Deliverable

Document the searchable grain, embedded text, model identity, persisted
artifacts, filter-before-rank behavior, and scaling threshold that would cause
the design to change.
