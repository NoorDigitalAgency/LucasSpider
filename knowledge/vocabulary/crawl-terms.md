---
schema_version: 1
kind: vocabulary
id: lucasspider-crawl-terms
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:39.731008+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/DataFlowContext.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Model.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/EntityBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/TableMetadata.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/RequestPolicy.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Response.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestHasher.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestedQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/SchedulerBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/ISelectable.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/DataParser`.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Crawl terms and source-local representations

Request is a work description with URI/method/content/headers plus routing, retry/depth and timeout fields. Owner is assigned from SpiderId.Id and routes responses; it is not authenticated caller, tenant ownership or permission to crawl. Hash depends on Owner, absolute URI, Method, RequestedTimes and Content; RequestHash correlates the response with pending work. Agent is the worker identity copied to a response and successful request, while Downloader is a routing/implementation name. [src/LucasSpider/Http/Request.cs:L1–L331](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L1-L331), [src/LucasSpider/Http/Response.cs:L1–L213](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Response.cs#L1-L213), [src/LucasSpider/Infrastructure/RequestHasher.cs:L1–L33](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/RequestHasher.cs#L1-L33), [src/LucasSpider/Spider.cs:L225–L230](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L225-L230), [src/LucasSpider/Agent/AgentService.cs:L146–L158](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L146-L158).

Scheduler is the undispatched frontier; RequestedQueue is pending work with timestamp-aware timeout callbacks; duplicate remover is a separate memory/probabilistic history. RetriedTimes is an admission ceiling on RequestedTimes, not a universal bound on every failure branch. Chained attempts agent-bound routing, but publishes to raw AgentId while the distributed agent subscribes to `LucasSpider_{AgentId}`; no matching consumer is established here. Random uses the downloader route. Speed/Batch are dispatch controls, not a proven simultaneous downloader limit. [src/LucasSpider/Scheduler/SchedulerBase.cs:L1–L129](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/SchedulerBase.cs#L1-L129), [src/LucasSpider/Infrastructure/RequestedQueue.cs:L1–L118](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/RequestedQueue.cs#L1-L118), [src/LucasSpider/Http/RequestPolicy.cs:L1–L15](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/RequestPolicy.cs#L1-L15), [src/LucasSpider/Spider.cs:L650–L702](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L650-L702), [src/LucasSpider/Spider.cs:L392–L399](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L392-L399).

DataFlowContext is the per-response scope carrying request/response/options/services, serialized bytes, mutable properties/data and FollowRequests. Selectable represents HTML/JSON/XML/text or unsupported content; Selector selects a node/value; Formatter transforms a field and can have side effects. Model<T> reflects extraction attributes. IEntity/TableMetadata/Column/Schema describe storage metadata, not inspected customer records or a deployed database schema. FollowRequests return through normal admission after successful ordered flows. [src/LucasSpider/DataFlow/DataFlowContext.cs:L1–L232](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/DataFlowContext.cs#L1-L232), [src/LucasSpider/Selector/ISelectable.cs:L1–L73](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/ISelectable.cs#L1-L73), [src/LucasSpider/DataFlow/Parser/Model.cs:L1–L110](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Model.cs#L1-L110), [src/LucasSpider/DataFlow/Parser/Formatter.cs:L1–L53](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatter.cs#L1-L53), [src/LucasSpider/DataFlow/Storage/EntityBase.cs:L1–L186](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/EntityBase.cs#L1-L186), [src/LucasSpider/DataFlow/Storage/TableMetadata.cs:L1–L79](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/TableMetadata.cs#L1-L79), [src/LucasSpider/Spider.cs:L363–L384](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L363-L384).

Names remain scoped to this library. No UI display-label mapping, cross-repository synonym, global identity equivalence, billing interpretation or package-to-consumer compatibility agreement was established. See [project navigation](../project.md) and [unknowns](../decisions/conflicts-and-open-questions.md).

Formatter source occurrences in !DEBUG and DEBUG are compile alternatives, with one call per arm. Retry admission and cleanup are separate transitions: the admitted same Request can remain shared with its disposing context until dequeue clones it. Request.Version is a model field without assignment in owned HTTP conversion; AdditionalHandlers is a fresh list per getter, not persistent builder storage. SQL metadata types/defaults and release stage/pack mode are source policy representations whose concrete contracts are linked from [extraction](../capabilities/entity-extraction.md), [cleanup](../capabilities/response-data-flow.md), [HTTP](../capabilities/http-download.md), [storage](../systems/entity-storage.md) and [release controls](../systems/build-package-boundaries.md). [src/LucasSpider/DataFlow/Parser/DataParser`.cs:L182–L233](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/DataParser`.cs#L182-L233), [src/LucasSpider/Http/Request.cs:L188–L304](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L188-L304), [src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs:L1–L67](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs#L1-L67), [src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs:L1–L62](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs#L1-L62).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
