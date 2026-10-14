---
schema_version: 1
kind: system
id: lucasspider-message-queue
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-14T02:05:11.715079+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/MessageExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/MessagePackSerializerExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/MessageQueueExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/HttpResponseMessageExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/AsyncMessageConsumer.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/AsyncMessageHandler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/IMessageQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/Message.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/MessageQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/Messages.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/Topics.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Transport, serialization, routing and consumer lifecycle

AddMessageQueue uses TryAdd for the owned MessageQueue singleton; CreateDefaultBuilder calls it, resolving the original draft’s uninspected-binding question. This implementation keeps Channel<byte[]> objects in a concurrent dictionary, creates unbounded channels, writes messages and reports IsDistributed false. The interface still permits external distributed implementations, which were not inspected. [src/LucasSpider/MessageQueue/ServiceCollectionExtensions.cs:L1–L14](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/ServiceCollectionExtensions.cs#L1-L14), [src/LucasSpider/Builder.cs:L82–L94](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Builder.cs#L82-L94), [src/LucasSpider/MessageQueue/MessageQueue.cs:L1–L73](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/MessageQueue.cs#L1-L73), [src/LucasSpider/MessageQueue/IMessageQueue.cs:L1–L17](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/IMessageQueue.cs#L1-L17).

ConsumeAsync rejects a consumer already marked Registered, obtains the queue, marks registration and connects OnClosing to CloseQueue. It starts an asynchronous read loop and starts separate asynchronous handler work per message; nested StartNew tasks are not explicitly unwrapped/joined as completed processing. Closing removes and completes the channel, suppressing completion errors; disposal completes remaining writers and clears the dictionary. InvokeAsync requires a Received handler and awaits the event delegate. Queue close is not a durable ack, poison-message retry policy or per-message work drain. [src/LucasSpider/MessageQueue/MessageQueue.cs:L1–L73](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/MessageQueue.cs#L1-L73), [src/LucasSpider/MessageQueue/AsyncMessageConsumer.cs:L1–L53](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/AsyncMessageConsumer.cs#L1-L53), [src/LucasSpider/MessageQueue/AsyncMessageHandler.cs:L1–L6](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/AsyncMessageHandler.cs#L1-L6).

PublishAsBytesAsync uses owned MessagePack typeless serialization with Lz4Block compression, then calls IMessageQueue.PublishAsync. DeserializeAsync reads a memory stream; its generic overload casts the returned object and can return null. Message, agent/spider exit/register/heartbeat and statistics DTOs carry routing IDs, timestamps, counts and timing representations. These schemas do not authenticate their sender or bound deserialization trust; external MessagePack internals and broker implementations are unknown boundaries. [src/LucasSpider/Extensions/MessagePackSerializerExtensions.cs:L1–L37](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/MessagePackSerializerExtensions.cs#L1-L37), [src/LucasSpider/Extensions/MessageQueueExtensions.cs:L1–L14](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/MessageQueueExtensions.cs#L1-L14), [src/LucasSpider/MessageQueue/Message.cs:L1–L15](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/Message.cs#L1-L15), [src/LucasSpider/MessageQueue/Messages.cs:L1–L120](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/Messages.cs#L1-L120), [src/LucasSpider/MessageQueue/Topics.cs:L1–L9](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/Topics.cs#L1-L9).

Spider timestamps and inserts pending work before publish. Without a bound Agent it routes by Downloader; a prior Agent plus Chained policy selects the agent-specific route, while Random returns to the downloader route. AgentService consumes its downloader route and, in distributed mode, its own route, downloads and returns a response to the Owner route. Spider removes that response’s RequestHash before running the successful response pipeline. Publish failure can therefore follow local pending-state insertion, and duplicate/late responses can lack a match. [src/LucasSpider/Spider.cs:L255–L360](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L255-L360), [src/LucasSpider/Spider.cs:L650–L702](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L650-L702), [src/LucasSpider/Agent/AgentService.cs:L47–L170](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L47-L170).

WhetherTimeout is named as a timeout test but returns whether elapsed seconds is less than its supplied threshold. No relied delivery/expiry path was inferred from the name. Process-local unbounded queues and asynchronous handlers provide no demonstrated hard backpressure, authentication, persisted recovery, exactly-once or distributed ordering guarantee. [src/LucasSpider/Extensions/MessageExtensions.cs:L1–L13](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/MessageExtensions.cs#L1-L13).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
