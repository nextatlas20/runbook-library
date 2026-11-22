---
service: media-transcode
title: Drain the transcode queue after a regional failover
owner: Sam Okafor
severity: P2
last_reviewed: 2026-02-02
---

## Symptoms

After a regional failover the transcode queue keeps growing because the new
region has no GPU workers registered.

## Detection

Check the worker registry for the active region; an empty GPU pool explains the
backlog on its own.

## Mitigation

1. Register the standby GPU pool with the transcode scheduler.
2. Raise the queue concurrency to the standby pool size.
3. Let the backlog drain before failing traffic back.

## Verification

Queue depth falling steadily and p95 transcode time back under ten minutes.
