---
name: batch-data-pipeline
description: Design, implement, or review a batch data pipeline with explicit source and output contracts, deterministic transformations, lineage, quality handling, stable identifiers, idempotent materialization, backfill planning, and reproducible verification. Use for bounded or scheduled batch workloads; use a streaming-specific workflow for continuously processed event streams.
---

# Batch Data Pipeline

Build or review a batch pipeline whose inputs, transformations, outputs, and
operating behavior are explicit and reproducible.

## Recommend the production target first

Treat stated requirements and the current sample volume as minimum
acceptance criteria, not as the design ceiling. When the user wants a
real-world solution, lead with the architecture best suited to credible
production volume, reliability, concurrency, and operating needs. Do not
prefer a weaker design merely because the checked-in dataset is small or the
initial implementation is intentionally bounded.

Separate the recommended target architecture from the way it can be exercised
locally. Local-machine constraints may justify a lightweight emulator, a
bounded verification path, or staged adoption, but they do not make that
compromise the preferred production design. Label compromises explicitly and
state the scale or operational threshold at which they fail.

## Discover the contract

Before changing code, identify:

- batch boundaries, source formats, required fields, and retained raw evidence;
- the grain and key of every output;
- business rules that decide inclusion, exclusion, or interpretation;
- quality failures that must be surfaced instead of silently corrected;
- full-refresh, incremental, retry, and backfill behavior; and
- the command and tests that constitute a complete run.

Treat repository documentation and tests as evidence, but reconcile them with
the implementation when they disagree. Report material ambiguity rather than
inventing a policy.

## Design for reliable batch processing

- Retain an immutable or lossless source layer with batch identity, source
  location, and a content hash.
- Derive stable identifiers from canonical business or source content, not
  runtime timestamps or row positions alone.
- Keep modeled facts linked to their source records.
- Make parsing and entity-resolution status observable.
- Quarantine or record invalid values; never fabricate a replacement merely
  to satisfy a non-null model.
- State every output table's grain and enforce uniqueness at that grain.
- Define rerun and retry semantics so partial failures cannot create duplicate
  or mixed-version outputs.
- Make the transaction grain explicit. When files commit independently, define
  whether an earlier file remains committed after a later failure and expose
  the freshness of downstream snapshots.
- Treat database commit and source-file movement as separate operations. Define
  a recoverable finalization state instead of assuming they are atomic.
- Make backfills explicit about input scope, code and schema versions, and the
  downstream data being replaced.

## Preserve reproducibility

Prefer deterministic ordering, explicit parsing rules, versioned policies,
atomic file replacement, and transactional table replacement. A repeat run
over unchanged inputs and configuration should not append duplicates or change
bytes unexpectedly.

When verifying a pipeline:

1. Run focused unit and contract tests.
2. Run the documented end-to-end command.
3. Check schemas, row counts, uniqueness, referential integrity, and quality
   issue counts.
4. Rerun with unchanged inputs and compare stable artifacts or checksums.
5. Exercise retry, incremental, or backfill behavior when the implementation
   supports it and the task puts it at risk.
6. Separate expected generated-output changes from unrelated working-tree
   changes.

Incremental ingestion does not imply every derived artifact can be appended.
Recompute or invalidate whole-corpus outputs—such as nearest-neighbor lists—when
a new record can change results for existing records.

Do not delete, reset, or overwrite user changes while trying to obtain a clean
verification baseline.

## Deliverable

Explain batch boundaries, grains, lineage, quality behavior, rerun semantics,
backfill behavior, and verification evidence. Call out non-idempotent outputs
and distinguish observed behavior from production recommendations.
