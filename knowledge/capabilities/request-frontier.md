---
schema_version: 1
kind: capability
id: lucasspider-request-frontier
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
  path: src/LucasSpider/Scheduler/SchedulerBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/Component/HashSetDuplicateRemover.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestHasher.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestedQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/DataFlowContext.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Request frontier and in-flight tracking

Admission assigns Request.Owner from SpiderId.Id, excludes over-limit retries, and applies the depth limit only when Options.Depth is positive. Evidence: `src/LucasSpider/Spider.cs:186–231`. Creating a follow request clones its parent, resets RequestedTimes and Hash, increments Depth, sets Speed and Timestamp, and replaces RequestUri. Evidence: `src/LucasSpider/DataFlow/DataFlowContext.cs:88–99`.

SchedulerBase computes a hash, calls the duplicate remover, and pushes requests that pass. The inspected RequestHasher serializes Owner, absolute URI, Method, RequestedTimes and Content to compute the hash; therefore this hash is not solely URL identity. Evidence: `src/LucasSpider/Scheduler/SchedulerBase.cs:111–127`, `src/LucasSpider/Infrastructure/RequestHasher.cs:19–29`.

HashSetDuplicateRemover uses an in-memory dictionary keyed by Request.Hash, validates that Owner matches its initialized spider ID, and supports whole-set or individual reset. This is a scheduling invariant, not demonstrated user authorization. Evidence: `src/LucasSpider/Scheduler/Component/HashSetDuplicateRemover.cs:13–39,50–68`.

QueueDistinctBfsScheduler keeps a List<Request>, takes from its front, removes those entries and returns clones. This describes this implementation only; no default scheduler selection is inferred. Evidence: `src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs:15–19,33–57`.

RequestedQueue separately tracks dispatched requests by hash, schedules a timeout using Timeout and Timestamp, matches responses by removing their RequestHash, and collects timed-out requests. Evidence: `src/LucasSpider/Infrastructure/RequestedQueue.cs:16–25,32–82`, `src/LucasSpider/Spider.cs:308–310,650–693`.

Confidence: high for the inspected implementations. Duplicate state and pending state are distinct concepts. Persistence, fairness, global deduplication, restart recovery and all scheduler variants are unverified. Related: [lifecycle](crawl-lifecycle.md), [terms](../vocabulary/crawl-terms.md).

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
