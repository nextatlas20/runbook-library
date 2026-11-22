---
service: notifications-worker
title: Notification retries exhausted for push channel
owner: jonas.berg
severity: P2
last_reviewed: 2026-02-10
---

## Symptoms

`notifications_delivery_failures_total{channel="push"}` spikes and the dead letter
queue grows by thousands of messages per minute.

## Detection

Sample the dead letter payloads. A uniform `410 Gone` response means the device
tokens are stale; a `503` means the push provider is degraded.

## Mitigation

1. Enable the token cleanup job so stale tokens stop being retried.
2. Switch the provider back to the secondary endpoint.
3. Replay the dead letter queue once the provider is healthy.

## Verification

Dead letter queue draining, and delivery success above 99% for ten minutes.
