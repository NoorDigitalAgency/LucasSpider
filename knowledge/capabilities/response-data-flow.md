---
schema_version: 1
kind: capability
id: lucasspider-response-data-flow
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:38.892297+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/DataFlow/DataFlowBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/DataFlowContext.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/IDataFlow.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/DataParser.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/ConsoleStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/EntityFileStorageBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/FileStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/FileStorageBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/ImageStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/JsonEntityFileStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/JsonFileStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/StorageUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/ByteArrayContentExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/StringExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/RequestSupplier/IRequestSupplier.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/ByteArrayContent.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/SchedulerBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueBfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Ordered response processing and ordinary output storage

A successful matched response creates a DI scope and DataFlowContext carrying the original request, response, options, services and serialized MessageBytes. Registered flows run in insertion order and share that context. Only after they finish are FollowRequests admitted, total/success statistics updated and scheduler SuccessAsync called. ExitException requests host exit; other exceptions call FailAsync and attempt re-enqueue without incrementing the download retry counter. Context disposal runs in finally and disposes request/response while clearing its dictionaries/message bytes. [src/LucasSpider/Spider.cs:L363–L403](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L363-L403), [src/LucasSpider/DataFlow/DataFlowContext.cs:L1–L232](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/DataFlowContext.cs#L1-L232).

DataParser validates the request, initializes Selectable only when absent, honors an explicit SelectableBuilder, otherwise classifies content into HTML or text JSON/XML/plain text with a NotSelectable fallback. It invokes the subclass ParseAsync before collecting follow queries. Valid follow requests receive current Owner and response Agent before entering the context; parser validity uses any registered required validator, with no validators permitting all requests. Selection/formatter/conversion exceptions can escape to the enclosing data-flow retry branch. [src/LucasSpider/DataFlow/Parser/DataParser.cs:L1–L193](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/DataParser.cs#L1-L193), [src/LucasSpider/Extensions/ByteArrayContentExtensions.cs:L1–L79](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/ByteArrayContentExtensions.cs#L1-L79), [src/LucasSpider/Extensions/StringExtensions.cs:L1–L71](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/StringExtensions.cs#L1-L71).

CreateNewRequest clones the current request, resets RequestedTimes and Hash, increments Depth, sets current speed/timestamp and replaces URI. This preserves method/content/headers/properties according to Request.Clone, rather than turning every discovered link into a fresh GET. AddParsedResult stores or appends entity lists keyed by CLR Type. GetData returns an immutable dictionary snapshot whose values remain shared references; context cloning copies request/response/message bytes and follow requests but property/data values remain shallow. [src/LucasSpider/DataFlow/DataFlowContext.cs:L65–L98](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/DataFlowContext.cs#L65-L98), [src/LucasSpider/DataFlow/DataFlowContext.cs:L147–L229](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/DataFlowContext.cs#L147-L229), [src/LucasSpider/Http/Request.cs:L258–L288](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L258-L288), [src/LucasSpider/DataFlow/Parser/DataParser.cs:L81–L101](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/DataParser.cs#L81-L101).

JsonFileStorage and FileStorage skip empty parsed data, create an owner-specific folder, use File.OpenWrite and WriteLineAsync, and serialize the current dictionary (FileStorage also includes the request URI). They do not establish append-only, atomic, cross-process or durable transactional output. ConsoleStorage prints parsed data. ImageStorage instead checks response bytes and configured filename extensions, creates owner/path-derived directories and writes bytes under a static lock; that lock is process-local and the owned path construction is not an output authorization or retention policy. [src/LucasSpider/DataFlow/Storage/JsonFileStorage.cs:L1–L37](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/JsonFileStorage.cs#L1-L37), [src/LucasSpider/DataFlow/Storage/FileStorage.cs:L1–L40](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/FileStorage.cs#L1-L40), [src/LucasSpider/DataFlow/Storage/FileStorageBase.cs:L1–L59](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/FileStorageBase.cs#L1-L59), [src/LucasSpider/DataFlow/Storage/ConsoleStorage.cs:L1–L41](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/ConsoleStorage.cs#L1-L41), [src/LucasSpider/DataFlow/Storage/ImageStorage.cs:L1–L66](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/ImageStorage.cs#L1-L66).

Default storage creation is an explicit helper invoked by a subclass, not automatic data-flow population. It resolves the configured CLR type, requires a factory method, invokes it with IConfiguration and casts the result to IDataFlow; missing type/method/result fail. InitializeDataFlowsAsync sets each logger, awaits initialization and records initialized parsers. Initialization failures stop the application but the method does not rethrow or immediately terminate the whole initialization loop. No flow means the crawl can still run without producing parsed storage. [src/LucasSpider/Spider.cs:L127–L129](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L127-L129), [src/LucasSpider/Spider.cs:L721–L748](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L721-L748), [src/LucasSpider/DataFlow/Storage/StorageUtilities.cs:L1–L42](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/StorageUtilities.cs#L1-L42).

See [entity extraction](entity-extraction.md), [selectors/formatters](../systems/selectors-and-formatters.md), [entity storage](../systems/entity-storage.md) and [retry lifecycle](crawl-lifecycle.md). Source-local hooks are extensibility, not proof of a deployed pipeline or output access control.

The generic failure branch re-admits the same Request reference held by DataFlowContext, without cloning or increasing RequestedTimes. SchedulerBase passes admitted work to the owned list schedulers, whose enqueue methods retain that reference and whose dequeue methods clone later. Finally disposes the context’s request, clearing Headers and Properties and disposing content. If retry admission succeeds and dequeue cloning has not already occurred, cleanup therefore mutates the queued request; ByteArrayContent.Dispose clears Bytes and a later clone dereferences its length. Duplicate rejection and timing can change this outcome; this is a conditional source interaction, not an observed race or a guarantee of retry corruption. [src/LucasSpider/Spider.cs:L363–L405](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L363-L405), [src/LucasSpider/DataFlow/DataFlowContext.cs:L52–L63](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/DataFlowContext.cs#L52-L63), [src/LucasSpider/DataFlow/DataFlowContext.cs:L192–L200](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/DataFlowContext.cs#L192-L200), [src/LucasSpider/Http/Request.cs:L291–L304](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L291-L304), [src/LucasSpider/Http/ByteArrayContent.cs:L24–L58](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/ByteArrayContent.cs#L24-L58), [src/LucasSpider/Scheduler/SchedulerBase.cs:L111–L127](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/SchedulerBase.cs#L111-L127), [src/LucasSpider/Scheduler/QueueBfsScheduler.cs:L1–L63](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueBfsScheduler.cs#L1-L63), [src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs:L1–L60](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs#L1-L60), [src/LucasSpider/Scheduler/QueueDfsScheduler.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDfsScheduler.cs#L1-L78), [src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs#L1-L78).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
