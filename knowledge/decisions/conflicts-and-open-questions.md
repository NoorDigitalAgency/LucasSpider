---
schema_version: 1
kind: decision
id: lucasspider-open-questions
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-14T02:05:11.715079+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/DataParser`.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/Download.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/EntityBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/JsonEntityFileStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/MessagePackSerializerExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/LRUCache.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/HeaderUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/PrintArgumentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/LucasSpider.csproj
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/MessageQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyBackgroundService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/Component/BloomFilterDuplicateRemover.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Source edge cases, unknown deployments and policy questions

Which scheduler/downloader/proxy/queue/storage composition does each environment use, and who can accept its facts? Source registrations are known; live composition and accepting authority are not. Which immutable implementation is consumed by each selected application? A reported LucasSpider 2026.1.0 declaration and this library’s package manifest are not an exact source pin. Microsoft.VisualBasic 10.3.0 is now verified as a public declaration, resolving package-presence uncertainty while leaving external implementation/source correspondence unknown. [src/LucasSpider/Builder.cs:L1–L178](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Builder.cs#L1-L178), [src/LucasSpider/LucasSpider.csproj:L1–L31](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/LucasSpider.csproj#L1-L31).

Should non-distinct DFS use the distinct implementation’s tail bound? Should Bloom duplicate reset retain the old counter, and how should completed-request reset interact with its unimplemented per-request reset? Should the data-flow exception attempt advance a separate retry counter or reset duplicate history? The actual source branches are documented; this knowledge proposal does not select intent or patch them. [src/LucasSpider/Scheduler/QueueDfsScheduler.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDfsScheduler.cs#L1-L78), [src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs#L1-L78), [src/LucasSpider/Scheduler/Component/BloomFilterDuplicateRemover.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/Component/BloomFilterDuplicateRemover.cs#L1-L78), [src/LucasSpider/Spider.cs:L392–L399](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L392-L399).

Should formatters run twice, missing global selections fail, and Download pass its arguments in the current order? Should CSS cache eviction remove two list entries, repeated entity metadata calls repopulate existing keys, and entity writers share a TypeName key across owners? Should relational storage propagate exhausted/caught write failures, implement duplicate-ignore separately and honor date postfixes in emitted table names? These static concerns require maintainer intent and suitable isolated validation, neither performed here. [src/LucasSpider/DataFlow/Parser/DataParser`.cs:L108–L229](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/DataParser%60.cs#L108-L229), [src/LucasSpider/DataFlow/Parser/Formatters/Download.cs:L1–L34](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/Download.cs#L1-L34), [src/LucasSpider/HtmlAgilityPack.Css/LRUCache.cs:L1–L132](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/HtmlAgilityPack.Css/LRUCache.cs#L1-L132), [src/LucasSpider/DataFlow/Storage/EntityBase.cs:L1–L186](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/EntityBase.cs#L1-L186), [src/LucasSpider/DataFlow/Storage/JsonEntityFileStorage.cs:L1–L53](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/JsonEntityFileStorage.cs#L1-L53), [src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs:L1–L278](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs#L1-L278), [src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs:L1–L426](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs#L1-L426).

What enforces destination/DNS/egress policy, credential/header forwarding, sender/deserialization trust, output permissions/path constraints and retention? Are URL/header/request/options logs redacted? What hard memory/concurrency/drain bounds apply to unbounded channels and spawned tasks? What proxy lease/wait/counter policy and cancellation behavior is intended? No actual credentials, payloads, logs, providers or deployed permissions were inspected. [src/LucasSpider/Http/Request.cs:L188–L238](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L188-L238), [src/LucasSpider/Http/HeaderUtilities.cs:L1–L30](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/HeaderUtilities.cs#L1-L30), [src/LucasSpider/MessageQueue/MessageQueue.cs:L1–L73](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/MessageQueue.cs#L1-L73), [src/LucasSpider/Extensions/MessagePackSerializerExtensions.cs:L1–L37](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/MessagePackSerializerExtensions.cs#L1-L37), [src/LucasSpider/Proxy/ProxyService.cs:L1–L146](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyService.cs#L1-L146), [src/LucasSpider/Proxy/ProxyBackgroundService.cs:L1–L64](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyBackgroundService.cs#L1-L64), [src/LucasSpider/Infrastructure/PrintArgumentService.cs:L1–L52](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/PrintArgumentService.cs#L1-L52).

The full production audit closes the old representative-source omissions but does not measure a semantic coverage percentage or test the application. Mixed fixtures/samples and external SDK/framework/provider/workflow sources remain explicit unknowns. Revalidate every affected record when authoritative answers, source changes, exact consumed pins or authorized deployment evidence become available.

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
