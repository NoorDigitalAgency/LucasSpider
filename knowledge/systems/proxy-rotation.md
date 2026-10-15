---
schema_version: 1
kind: system
id: lucasspider-proxy-rotation
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-14T02:05:11.715079+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Agent/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/HttpClientDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/DefaultProxyValidator.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/EmptyProxyService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/EmptyProxySupplier.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/FakeProxyValidator.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/FiddlerProxySupplier.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/IProxyService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/IProxySupplier.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/IProxyValidator.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/KuaidailiProxySupplier.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyBackgroundService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyHttpClientHandler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Proxy supply, validation, leasing and handler feedback

UseProxy/AddProxy register a supplier, validator, ProxyService, background supplier service and selected HttpMessageHandlerBuilder; simpler overloads choose DefaultProxyValidator and ProxyHttpMessageHandlerBuilder. The normal agent registration initially uses TryAdd for EmptyProxyService, and HttpClientDownloader selects proxy mode when its injected service is not that empty implementation. Unknown external composition is not inferred from these owned registrations. [src/LucasSpider/Proxy/ServiceCollectionExtensions.cs:L1–L80](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ServiceCollectionExtensions.cs#L1-L80), [src/LucasSpider/Agent/ServiceCollectionExtensions.cs:L1–L28](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/ServiceCollectionExtensions.cs#L1-L28), [src/LucasSpider/Downloader/HttpClientDownloader.cs:L24–L33](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/HttpClientDownloader.cs#L24-L33).

ProxyBackgroundService resolves a supplier, fails if absent, then repeatedly fetches and validates/adds proxies with RefreshProxy-derived delay. Its failure counter is declared inside the while loop, so repeated failures never reach the apparent break condition. The delay is inside try, not catch; a persistent supplier failure loops immediately without backoff. Successful-iteration delays use the default token. EmptyProxySupplier yields none; FiddlerProxySupplier yields a configured URI once, while KuaidailiProxySupplier retrieves/parses a configured supplier response. Source default URLs and endpoint contents are withheld; no supplier service was contacted. [src/LucasSpider/Proxy/ProxyBackgroundService.cs:L1–L64](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyBackgroundService.cs#L1-L64), [src/LucasSpider/Proxy/EmptyProxySupplier.cs:L1–L15](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/EmptyProxySupplier.cs#L1-L15), [src/LucasSpider/Proxy/FiddlerProxySupplier.cs:L1–L30](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/FiddlerProxySupplier.cs#L1-L30), [src/LucasSpider/Proxy/KuaidailiProxySupplier.cs:L1–L31](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/KuaidailiProxySupplier.cs#L1-L31), [src/LucasSpider/Proxy/ProxyOptions.cs:L1–L16](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyOptions.cs#L1-L16).

ProxyService validates candidates, deduplicates by URI and queues entries. Get dequeues and schedules a timed successful return; GetAsync polls with its argument interpreted as seconds. HttpClientDownloader passes Request.Timeout in milliseconds to that seconds argument. At the default 30,000 ms, an empty pool polls 300,000 times at 100 ms each, about 30,000 seconds (8.3 hours), while the spider's pending queue can time out and retry the request after 30 seconds. ReturnAsync resets/increments failures, drops entries beyond the threshold or on periodic failed revalidation, otherwise re-enqueues. The timer and handler can both return a lease; no exclusive single-return flag exists in these owned paths. [src/LucasSpider/Proxy/ProxyService.cs:L1–L146](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyService.cs#L1-L146), [src/LucasSpider/Downloader/HttpClientDownloader.cs:L160–L185](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/HttpClientDownloader.cs#L160-L185), [src/LucasSpider/Http/Request.cs:L45–L51](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L45-L51).

DefaultProxyValidator requires a syntactically valid test URI, creates a proxy-named client, sends HEAD with a technical test marker, returns the success status predicate and catches request errors as false. FakeProxyValidator always returns true. ProxyHttpClientHandler strips the test marker and returns non-test proxies in finally using the response status or BadGateway on failure. The proxy handler builder requires its technical name prefix, constructs WebProxy and decompression/certificate settings. EmptyProxyService methods throw if invoked; it is a sentinel for direct mode, not an operational pool. [src/LucasSpider/Proxy/DefaultProxyValidator.cs:L1–L56](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/DefaultProxyValidator.cs#L1-L56), [src/LucasSpider/Proxy/FakeProxyValidator.cs:L1–L13](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/FakeProxyValidator.cs#L1-L13), [src/LucasSpider/Proxy/ProxyHttpClientHandler.cs:L1–L39](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyHttpClientHandler.cs#L1-L39), [src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs:L1–L62](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs#L1-L62), [src/LucasSpider/Proxy/EmptyProxyService.cs:L1–L30](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/EmptyProxyService.cs#L1-L30).

Pool state is process memory and validation only observes the configured request’s outcome if run. Proxy authentication, destination authority, timer shutdown, supplier trust, endpoint availability, fairness and deployed credentials are unknown. See [HTTP handler composition](../capabilities/http-download.md) and [PPPoE alternative](../capabilities/browser-file-download.md).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
