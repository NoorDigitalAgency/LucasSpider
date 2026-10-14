---
schema_version: 1
kind: capability
id: lucasspider-crawl-lifecycle
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:39.140054+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestedQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/SpiderOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/DataFlowContext.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Dispatch, retries, completion and shutdown

Admission supplies a missing downloader, requires a request-specific pattern for the PPPoE downloader family, drops requests whose RequestedTimes exceeds RetriedTimes and applies a positive-only depth ceiling before assigning Owner from SpiderId. Dispatch records the host, calls ConfigureRequest, checks the registered parsers, waits on the token bucket and publishes scheduler batches. When there are no initialized parsers, its validity gate permits requests; otherwise any parser validator can admit one. [src/LucasSpider/Spider.cs:L186–L230](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L186-L230), [src/LucasSpider/Spider.cs:L412–L419](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L412-L419), [src/LucasSpider/Spider.cs:L427–L519](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L427-L519).

Source defaults are Speed 1, Batch 4, RequestedQueueCount 1000, RetriedTimes 3 and DefaultTimeout 30000 milliseconds. Constructor checks reject Speed above 500 or below 0.01 and DefaultTimeout below 2000; dispatch also clamps speed when reading it. The pending-count gate uses greater-than, so it is not a strict ceiling at equality. Batch and speed control dispatch, not a proven maximum number of concurrent downloads: agent handling starts untracked asynchronous work. [src/LucasSpider/SpiderOptions.cs:L10–L56](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/SpiderOptions.cs#L10-L56), [src/LucasSpider/Spider.cs:L73–L105](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L73-L105), [src/LucasSpider/Spider.cs:L422–L424](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L422-L424), [src/LucasSpider/Spider.cs:L440–L470](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L440-L470), [src/LucasSpider/Agent/AgentService.cs:L146–L170](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L146-L170).

The response callback catches deserialization failures and ignores null messages. A matching exit message stops this spider. Responses remove pending work by RequestHash; success transfers Agent and runs data flows, while a non-success response increments RequestedTimes, re-enqueues and invokes OnRequestError. Unmatched responses do not enter that matched branch. Completed-request duplicate reset, when enabled, follows response handling; the response count then advances. [src/LucasSpider/Spider.cs:L255–L360](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L255-L360).

Timeout callbacks remove only the pending entry with the same hash and timestamp. Timeout collection increments RequestedTimes and response accounting, optionally resets duplicate checks, re-enqueues and invokes OnRequestTimeout. This is separate from the data-flow exception branch: that branch calls scheduler failure and attempts re-enqueue without incrementing RequestedTimes. With distinct hashing, existing duplicate state can suppress that attempt; with other compositions it need not be bounded by the download counter. [src/LucasSpider/Infrastructure/RequestedQueue.cs:L1–L118](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/RequestedQueue.cs#L1-L118), [src/LucasSpider/Spider.cs:L363–L403](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L363-L403), [src/LucasSpider/Spider.cs:L566–L592](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L566-L592).

DownloadsRemaining uses request/response counts or a computed elapsed-time allowance based on observed hosts and outstanding work. Empty scheduler handling invokes OnSchedulerEmpty and uses EmptySleepTime before ending; wait/throttle delays often pass the default token rather than the host token. RunAsync catches failures and always calls ExitAsync, which reports exit then stops the host. StopAsync closes the response consumer/queue, awaits the base stop and disposes pending work, data flows, queue and scheduler; it does not explicitly join the agent’s spawned download tasks. [src/LucasSpider/Spider.cs:L521–L646](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L521-L646), [src/LucasSpider/Spider.cs:L132–L139](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L132-L139), [src/LucasSpider/Spider.cs:L752–L760](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L752-L760), [src/LucasSpider/Agent/AgentService.cs:L195–L229](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L195-L229).

These are static branches, not a promise of complete crawling, exactly-once execution, durable restart, timing precision or a hard shutdown bound. See [frontier](request-frontier.md), [data-flow retries](response-data-flow.md) and [transport](../systems/message-queue.md).

Data-flow retry admission passes the same request reference into the scheduler before context cleanup. If admitted and still queued, its headers/properties/content can be changed by that cleanup before dequeue clones it. This is distinct from retry-count/dedup policy and depends on admission and timing; see [response data flow](response-data-flow.md). [src/LucasSpider/Spider.cs:L363–L405](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L363-L405), [src/LucasSpider/DataFlow/DataFlowContext.cs:L192–L200](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/DataFlowContext.cs#L192-L200), [src/LucasSpider/Http/Request.cs:L291–L304](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L291-L304).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
