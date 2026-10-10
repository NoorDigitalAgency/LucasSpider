---
schema_version: 1
kind: capability
id: lucasspider-crawl-lifecycle
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-10T03:20:42+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/SpiderOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Dispatch, completion and retry lifecycle

The dispatch loop reads `Options.Batch` scheduler requests, calls `ConfigureRequest`, validates requests against the registered parsers, waits on a token bucket, and publishes each accepted request. `RequestedQueueCount` gates dispatch when the in-flight count is greater than the configured value. Evidence: `src/LucasSpider/Spider.cs:427–547`; parser-based validation: `src/LucasSpider/Spider.cs:407–425`.

Constructor validation rejects Speed above 500 or below 0.01 and DefaultTimeout below 2000. Source defaults include Speed 1, Batch 4, RequestedQueueCount 1000, RetriedTimes 3 and DefaultTimeout 30000. These are source defaults, not observed deployment settings. Evidence: `src/LucasSpider/Spider.cs:78–96`, `src/LucasSpider/SpiderOptions.cs:10–35,56`.

A non-success response increments RequestedTimes and re-enqueues the matched request; timeout collection also increments RequestedTimes and re-enqueues. Admission drops requests when RequestedTimes exceeds RetriedTimes. Evidence: `src/LucasSpider/Spider.cs:308–339,212–216,566–592`. Data-flow exceptions also attempt re-enqueue but this branch does not increment RequestedTimes; it must not be described as the same retry counter behavior. Evidence: `src/LucasSpider/Spider.cs:392–399`.

`DownloadsRemaining` uses response/request counts or elapsed time; idle waiting eventually exits, and `ExitAsync` stops the host application. Evidence: `src/LucasSpider/Spider.cs:549–563,595–613,630–634`.

Confidence: high for static control flow. Speed and Batch regulate dispatch; they do not prove a hard maximum number of simultaneous downloads. Agent request handling starts asynchronous tasks, and this excerpt establishes no semaphore bound. Evidence: `src/LucasSpider/Agent/AgentService.cs:146–170`. No guarantee of complete crawling, exactly-once handling, timing precision, durable recovery or production throughput is established. Related: [frontier](request-frontier.md), [queue](../systems/message-queue.md).

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
