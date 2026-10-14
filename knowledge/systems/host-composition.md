---
schema_version: 1
kind: system
id: lucasspider-host-composition
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:39.804363+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Agent/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/StorageUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DependenceServices.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/DockerLifeTime.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/ObjectUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/PrintArgumentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/SpiderOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Host configuration, service resolution and disposal

Builder.CreateBuilder accepts a Spider type plus optional arguments/options callback, configures the host and registers that type as IHostedService. ConfigureBuilder sets the current content root, loads host environment/command-line inputs, optional base/environment JSON configuration, development user secrets, environment variables and command-line values. The callback configures SpiderOptions after configuration binding. These are source input channels; no actual settings, secrets or environment values were inspected. [src/LucasSpider/Builder.cs:L1–L178](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Builder.cs#L1-L178).

Common registrations add HTTP clients, PrintArgumentService, the default HttpClientDownloader agent, statistics client, DependenceServices, request hashing and Murmur hashing. Development enables service-provider scope/build validation. CreateDefaultBuilder adds the local queue and DefaultStatisticsStore/service but does not itself select a scheduler or add data flows; source scheduler/downloader/proxy/storage extensions compose those separately. TryAddSingleton and AddSingleton choices differ, so extra caller registrations remain a composition boundary. [src/LucasSpider/Builder.cs:L82–L94](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Builder.cs#L82-L94), [src/LucasSpider/Builder.cs:L150–L175](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Builder.cs#L150-L175), [src/LucasSpider/Agent/ServiceCollectionExtensions.cs:L1–L28](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/ServiceCollectionExtensions.cs#L1-L28), [src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs:L1–L35](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs#L1-L35), [src/LucasSpider/Downloader/ServiceCollectionExtensions.cs:L1–L76](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/ServiceCollectionExtensions.cs#L1-L76).

DependenceServices groups the service provider, selected scheduler/queue/statistics/lifetime/configuration/context and disposes the queue/scheduler. Spider disposes that aggregate, pending queue and flows using ObjectUtilities, which suppresses disposal exceptions (optionally logging). UseDockerLifetime registers an IHostLifetime whose stop path calls Environment.Exit; it is a source process-control option, not a graceful-drain or deployment guarantee. PrintArgumentService reflects and logs SpiderOptions plus assembly version at startup, requiring configuration/logging review. [src/LucasSpider/DependenceServices.cs:L1–L45](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DependenceServices.cs#L1-L45), [src/LucasSpider/Spider.cs:L752–L760](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L752-L760), [src/LucasSpider/Infrastructure/ObjectUtilities.cs:L1–L57](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/ObjectUtilities.cs#L1-L57), [src/LucasSpider/ServiceCollectionExtensions.cs:L63–L66](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/ServiceCollectionExtensions.cs#L63-L66), [src/LucasSpider/Infrastructure/DockerLifeTime.cs:L1–L21](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DockerLifeTime.cs#L1-L21), [src/LucasSpider/Infrastructure/PrintArgumentService.cs:L1–L52](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/PrintArgumentService.cs#L1-L52).

Options are mutable source configuration: dispatch can refresh batch/speed, while construction captures other dependencies and downloader choice. SpiderOptions.Clone is MemberwiseClone. Reflection-selected storage and request-specific PPPoE pattern are explicit helper contracts, not automatic operating policy. Configuration shape changes, registration order and extension hooks invalidate the affected knowledge; live values and app-specific scopes are unknown. [src/LucasSpider/SpiderOptions.cs:L1–L74](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/SpiderOptions.cs#L1-L74), [src/LucasSpider/Spider.cs:L103–L105](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L103-L105), [src/LucasSpider/Spider.cs:L465–L505](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L465-L505), [src/LucasSpider/DataFlow/Storage/StorageUtilities.cs:L1–L42](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/StorageUtilities.cs#L1-L42).

HTTP builder composition has an additional local limit: AdditionalHandlers returns a fresh list on every access in both owned builders. A supplied default primary handler is still cast to HttpClientHandler for redirect setup; a supplied proxy primary handler instead takes an immediate pipeline branch that skips owned proxy/cookie/decompression/certificate configuration. Newly created owned handlers enable cookies. See [HTTP composition](../capabilities/http-download.md) for input/effect/failure boundaries; actual external registrations and wire/session behavior remain unknown. [src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs:L1–L67](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs#L1-L67), [src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs:L1–L62](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs#L1-L62).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
