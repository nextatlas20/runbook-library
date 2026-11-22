---
service: checkout-web
title: Checkout latency above 2 seconds
owner: Marco Silva
severity: P1
last_reviewed: 2026-01-15
---

## Symptoms

`checkout_http_request_duration_seconds{p99}` stays above 2.0 for more than ten
minutes and the conversion alert fires in the same window.

## Detection

Compare the p99 latency panel against the upstream `payments-api` latency panel.
If payments is healthy while checkout is slow, the regression is on our side.

## Mitigation

1. Flip `checkout.quote_cache` to `enabled` in the runtime config.
2. Drain the two slowest pods with `kubectl rollout restart deploy/checkout-web`.
3. If latency is still high, enable the degraded quote path so customers can
   still pay with a stored card.

## Verification

p99 back under 800 ms for fifteen consecutive minutes, and the conversion alert
clears on its own.
