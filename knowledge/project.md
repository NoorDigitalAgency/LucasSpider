---
schema_version: 1
kind: project
id: lucasspider-project
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:39.791574+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestHasher.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# LucasSpider: crawl host, frontier, workers and extraction

LucasSpider is an extensible crawling library. A supplied Spider subclass provides InitializeAsync; Builder registers it as an IHostedService and composes the downloader agent, hashing and configuration services. CreateDefaultBuilder additionally registers the owned in-process message queue and statistics store/service. A scheduler still needs an explicit registration. These are owned registration contracts; a caller can compose additional or replacement services. [src/LucasSpider/Builder.cs:L69–L94](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Builder.cs#L69-L94), [src/LucasSpider/Builder.cs:L150–L175](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Builder.cs#L150-L175), [src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs:L1–L35](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs#L1-L35), [src/LucasSpider/MessageQueue/ServiceCollectionExtensions.cs:L1–L14](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/ServiceCollectionExtensions.cs#L1-L14).

The crawl begins by generating its routing identity, starting statistics, initializing the scheduler, invoking the subclass initializer, initializing data flows, loading suppliers and registering response consumption before dispatch. Requests pass through admission, hashing/deduplication, pending timeout tracking, serialization and an agent downloader; correlated responses run ordered data flows and admit follow requests. [src/LucasSpider/Spider.cs:L234–L252](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L234-L252), [src/LucasSpider/Spider.cs:L363–L403](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L363-L403), [src/LucasSpider/Spider.cs:L650–L718](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L650-L718), [src/LucasSpider/Infrastructure/RequestHasher.cs:L1–L33](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/RequestHasher.cs#L1-L33).

Navigate by task: [host composition](systems/host-composition.md), [crawl lifecycle](capabilities/crawl-lifecycle.md), [request frontier](capabilities/request-frontier.md), [HTTP download](capabilities/http-download.md), [browser/file alternatives](capabilities/browser-file-download.md), [response data flow](capabilities/response-data-flow.md), [entity extraction](capabilities/entity-extraction.md), [selectors and formatters](systems/selectors-and-formatters.md), [entity persistence](systems/entity-storage.md), [proxy rotation](systems/proxy-rotation.md), [message transport](systems/message-queue.md), [agents and statistics](systems/agents-and-statistics.md), [request/response models](systems/request-response-models.md), [build and dependency boundaries](systems/build-package-boundaries.md), [terms](vocabulary/crawl-terms.md), [stewardship](governance/ownership.md) and [open questions](decisions/conflicts-and-open-questions.md).

Source scope is commit 495ed7cc49208acaa50de7dcf5ebdec584394000. Its committer evidence time is 2026-04-07T12:57:08+02:00, independently checked from Git metadata; last_verified records the present static audit, and deployment effective time is unknown. The full tracked inventory has 252 paths: all 205 production C# files and 16 technical texts were privately read to EOF. The 24 mixed test/sample C# files and seven fixture/config/opaque paths remain metadata-only boundaries. Supporting matrices retain every path, directory, native operation and typed member; counts do not establish runtime coverage.

All records remain proposed. Exact consumed implementation revisions, live composition, package publication, output permissions and accepting authority remain unknown. The separately reported consumer declaration LucasSpider 2026.1.0 does not identify the immutable implementation consumed by Lucas; this audit does not substitute the current sibling source or inspect consumer/package implementation. Confidence is high for pinned owned static contracts and limited at those boundaries.

Behavioral edge contracts are findable in the task records: mutually exclusive formatter compile arms and concrete selector/time outputs; conditional Linux redial failure; same-reference retry admission followed by cleanup; concrete SQL types/defaults; stored versus applied HTTP version and handler-list composition; and manual release input/pack branches. These are pinned source contracts, with compiler/framework/provider/process/workflow outcomes qualified at their boundaries. See [extraction](capabilities/entity-extraction.md), [selectors](systems/selectors-and-formatters.md), [downloaders](capabilities/browser-file-download.md), [cleanup](capabilities/response-data-flow.md), [SQL generation](systems/entity-storage.md), [HTTP](capabilities/http-download.md) and [release controls](systems/build-package-boundaries.md).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
