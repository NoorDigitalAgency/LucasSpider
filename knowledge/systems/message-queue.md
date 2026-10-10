---
schema_version: 1
kind: system
id: lucasspider-message-queue
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-10T03:20:42+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/MessageQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/IMessageQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Message transport boundary

The inspected MessageQueue implementation stores Channel<byte[]> instances in a ConcurrentDictionary, creates channels with CreateUnbounded, publishes byte messages and dispatches consumers asynchronously. It returns IsDistributed=false. CloseQueue removes and completes a channel; Dispose completes remaining channels and clears the dictionary. Evidence: `src/LucasSpider/MessageQueue/MessageQueue.cs:10–72`.

The IMessageQueue abstraction exposes publish, consume, close and IsDistributed. Builder.CreateDefaultBuilder invokes AddMessageQueue; that extension's implementation was not inspected, so this record does not assert the runtime/default binding. Evidence: `src/LucasSpider/MessageQueue/IMessageQueue.cs:7–15`, `src/LucasSpider/Builder.cs:82–94`.

Within the inspected flow, Spider publishes requests after tracking them in RequestedQueue; AgentService downloads them and routes responses back using Request.Owner; Spider consumes the response and correlates it by RequestHash. Evidence: `src/LucasSpider/Spider.cs:255–360,650–693`, `src/LucasSpider/Agent/AgentService.cs:110–115,146–170`.

Confidence: high for the inspected implementation and call sites. The abstract distributed flag and distributed branches do not establish a deployed broker, broker authentication, durable delivery, bounded memory/backpressure or exactly-once processing. Channel names and serialized payload schemas are sensitive technical metadata; no live queue or payload was inspected. Related: [lifecycle](../capabilities/crawl-lifecycle.md), [terms](../vocabulary/crawl-terms.md).

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
