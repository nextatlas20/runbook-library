---
service: payments-api
title: Card capture failures on the authorise call
owner: Dana Whitfield
severity: P2
last_reviewed: 2025-09-02
---

## Symptoms

`payments_capture_errors_total` climbs while authorisation volume is flat, and
merchants report declined cards that their processor never saw.

## Detection

Filter the capture log for `status=upstream_timeout`. A burst that tracks one
acquirer points at that acquirer's sandbox, not at our retry loop.

## Mitigation

1. Disable the failing acquirer in `payments.routing.weights`.
2. Replay the stuck capture batch with `payments-cli capture --replay 15m`.
3. Confirm the ledger does not hold duplicate captures before replaying again.

## Verification

Capture error rate below 0.2% for twenty minutes and no new entries in the
reconciliation backlog.
