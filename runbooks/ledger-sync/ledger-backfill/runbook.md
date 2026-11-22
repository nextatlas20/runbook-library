---
service: ledger-sync
title: Ledger backfill fell behind
owner: Aiko Tanaka
severity: P1
last_reviewed: 2025-12-20
---

## Symptoms

`ledger_backfill_lag_seconds` grows past one hour and the finance dashboard shows
a gap between settled payments and posted journal entries.

## Detection

Check the backfill worker's checkpoint offset against the payment event stream.
A frozen offset means the worker is wedged; a growing offset means it is simply
too slow.

## Mitigation

1. Restart the backfill worker with `kubectl rollout restart deploy/ledger-backfill`.
2. If the offset is frozen again within ten minutes, switch the worker to the
   `bulk` profile so it consumes 5k events per batch.
3. Never truncate the checkpoint table; the replay is resumable.

## Verification

Lag under five minutes and the finance reconciliation diff back to zero.
