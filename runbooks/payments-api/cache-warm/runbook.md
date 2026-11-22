---
service: payments-api
title: Warm the card vault cache after a deploy
owner: Dana Whitfield
severity: S2
last_reviewed: 2025-11-05
---

## Symptoms

Immediately after a deploy, card token lookups take 400 ms instead of 12 ms and
the authorise endpoint approaches its timeout budget.

## Detection

The vault cache hit ratio drops to zero right after the pods roll; it recovers on
its own after roughly twenty minutes.

## Mitigation

1. Run `payments-cli vault warm --shards 8` after every deploy of `payments-api`.
2. Keep the cache warm-up in the deploy pipeline rather than doing it by hand.

## Verification

Vault cache hit ratio above 95% within two minutes of the deploy finishing.
