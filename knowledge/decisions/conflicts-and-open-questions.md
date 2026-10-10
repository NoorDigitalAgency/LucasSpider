---
schema_version: 1
kind: decision
id: lucasspider-open-questions
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
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/HttpClientDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/MessageQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Conflicts and open questions

No cross-repository vocabulary agreement is established. The crawler associates Lucas with this target, but its exact consumed source revision is unknown; consumer source and consumer knowledge were not inspected. The crawler lists nuget:Microsoft.VisualBasic as unresolved; no external source was inspected and package presence/version does not establish an exact source pin.

Questions for the reviewer:

- Who currently owns this library and who may accept its facts? Historical contribution alone is insufficient.
- Which revision is actually consumed by each selected application, and what terminology/routing/data contract exists there?
- Which scheduler, downloader, proxy, message queue and storage are bound in each environment? Builder extensibility is visible, not a deployment inventory (`src/LucasSpider/Builder.cs:69–94,96–176`).
- What enforces crawl destination, credential/header forwarding, caller/resource permissions, output access and retention? Request.Owner assignment and request header forwarding are visible, but authorization is not demonstrated (`src/LucasSpider/Spider.cs:225`, `src/LucasSpider/Http/Request.cs:188–238`, `src/LucasSpider/Downloader/HttpClientDownloader.cs:75–89`).
- Are URLs, headers and serialized requests redacted in deployment logs? URL and request serialization paths are present (`src/LucasSpider/Downloader/HttpClientDownloader.cs:54–65,98–110`, `src/LucasSpider/Spider.cs:392–399`). No log contents were inspected.
- What workload limits apply beyond dispatch throttling, and how are in-process unbounded channels protected operationally? (`src/LucasSpider/Spider.cs:427–547`, `src/LucasSpider/MessageQueue/MessageQueue.cs:14–44`).
- Does the data-flow exception retry branch need a separately bounded retry policy? It re-enqueues without incrementing RequestedTimes in that branch (`src/LucasSpider/Spider.cs:392–399`). This is a source observation, not a reproduced defect.

Confidence: high for cited static observations; answers remain unknown. No external/global synonym, runtime guarantee or MCP capability is proposed. Revalidate every affected record when these questions gain evidence.

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
