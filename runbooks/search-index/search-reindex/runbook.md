---
service: search-index
title: Search reindex queue is not draining
owner: Priya Raman
severity: P2
last_reviewed: 2025-09-01
---

## Symptoms

`search_reindex_queue_depth` grows monotonically and freshly edited documents do
not appear in results for hours.

## Detection

Look at the indexer's worker count and the shard assignment table. A single hot
shard with a stuck merge is the usual cause.

## Mitigation

1. Pause the reindex consumer for the hot shard.
2. Force a merge on that shard with the index admin tool.
3. Resume the consumer and watch the queue depth fall.

## Verification

Queue depth under 10k and a fresh document visible within two minutes.
