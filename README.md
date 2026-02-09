# TurboLynx

**TurboLynx** is a native graph analytics system for **schemaless property graphs**.  
It is designed to keep graph-native flexibility while delivering strong performance for analytics (e.g., filtering, group-by, aggregation, and multi-hop traversal).

## Why TurboLynx?

Modern property graph workloads are often schemaless and highly heterogeneous.  
Existing approaches usually force a trade-off:

- **Native GDBMSes**: good traversal performance, but weaker analytics optimization.
- **RDBMS-based graph layers**: stronger optimizer reuse, but less schema flexibility and graph-native efficiency.

TurboLynx targets both: **native graph execution + mature analytics-oriented optimization**.

## Core Ideas

1. **Graphlet-based columnar storage**  
   - Groups similar schemas into coarse units called **graphlets** (cost-based merging).
   - Avoids per-tuple schema interpretation overhead.
   - Enables vectorized processing and faster attribute access.

2. **Metadata-aware indexing**  
   - Uses inverted indexes over attribute metadata to accelerate selective predicate filtering.

3. **Multi-schema query processing**  
   - Operators are extended to process vertices/edges from multiple graphlets.
   - Introduces **SSRF (Shared Schema Row Format)** with a unified header to control schema blow-up and null-handling overhead.
   - Uses a hybrid layout (columnar + selective row-style storage for sparse attributes).

4. **Graph-aware cost-based optimization**  
   - Adapts the **Orca** optimizer with graph-specific operators, rules, and cost models.
   - Adds an **early-merging strategy** (GOO-inspired) to reduce plan search space before join enumeration.

## What TurboLynx Is Good At

- Large, heterogeneous property graphs
- Workloads mixing traversal and analytics
- Read-heavy analytical scenarios with batch updates

## Summary

TurboLynx is an end-to-end design for schemaless graph analytics across:

- **Storage**
- **Execution**
- **Optimization**

The goal is simple: keep property-graph flexibility **without sacrificing analytical performance**.
