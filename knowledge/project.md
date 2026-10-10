---
schema_version: 1
kind: project
id: lucasspider-project
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-10T03:20:42+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# LucasSpider

LucasSpider exposes an extensible crawling host: `Builder.CreateBuilder` registers a supplied Spider type as an `IHostedService`; `CreateDefaultBuilder` additionally registers message queue and statistics services. `Spider` derives from `BackgroundService` and requires an `InitializeAsync` implementation. Evidence: `src/LucasSpider/Builder.cs:69–94`, `src/LucasSpider/Spider.cs:26–27,113`.

The inspected lifecycle initializes the scheduler, invokes the subclass initializer, initializes data flows, loads request suppliers, registers response consumption, and enters dispatch. Evidence: `src/LucasSpider/Spider.cs:234–252`.

Scope: this pinned library source, not a deployed crawl, consumer application, or current package release. Source effective time is the commit timestamp 2026-04-07T12:57:08+02:00; actual deployment effective time is unknown. Lucas consumer compatibility and its consumed source pin remain unknown; no consumer source or KB was read.

Confidence: high for the cited static structure; runtime behavior and deployment are unverified. Related records: [crawl lifecycle](capabilities/crawl-lifecycle.md), [frontier](capabilities/request-frontier.md), [data flow](capabilities/response-data-flow.md), [download](capabilities/http-download.md), [queue](systems/message-queue.md).

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
