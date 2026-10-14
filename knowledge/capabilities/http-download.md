---
schema_version: 1
kind: capability
id: lucasspider-http-download
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:39.411225+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/DownloaderOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/HttpClientDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/UriExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/ExtraHttpStatusCode.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/HeaderUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/HttpResponseMessageExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Response.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PPPoEService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PPPoEHttpClientDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# HTTP conversion, redirects and failure responses

AgentService invokes its injected IDownloader, returns without publishing if it yields null, otherwise assigns response.Agent and publishes to the request Owner route. HttpClientDownloader converts the request, chooses a host-named client or asks the proxy service for one, sets client timeout from Request.Timeout and adds the supplied UserAgent. Its send hook uses ResponseHeadersRead without a caller cancellation token. [src/LucasSpider/Agent/AgentService.cs:L146–L170](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L146-L170), [src/LucasSpider/Downloader/HttpClientDownloader.cs:L36–L75](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/HttpClientDownloader.cs#L36-L75), [src/LucasSpider/Downloader/HttpClientDownloader.cs:L154–L190](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/HttpClientDownloader.cs#L154-L190).

The manual redirect loop treats status 301 through 308 with a Location as redirecting, up to MaximumAllowedRedirects (source default 5). It clones the original request for each hop and resolves a relative Location against the original request URI, preserving the original method/content/headers; this is not a general browser redirect policy or a credential stripping contract. Exceeding the limit returns a failed response. The owned default handler separately sets AllowAutoRedirect to the inverse of TrackRedirects and applies the framework automatic redirect limit; the proxy handler builder does not set those two properties. Therefore manual-hop visibility depends on the actual handler composition. [src/LucasSpider/Downloader/HttpClientDownloader.cs:L76–L122](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/HttpClientDownloader.cs#L76-L122), [src/LucasSpider/Downloader/DownloaderOptions.cs:L1–L29](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/DownloaderOptions.cs#L1-L29), [src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs:L1–L67](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs#L1-L67), [src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs:L1–L62](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs#L1-L62), [src/LucasSpider/Extensions/UriExtensions.cs:L1–L12](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/UriExtensions.cs#L1-L12).

On the ordinary path the downloader buffers content through ToResponseAsync and sets RequestHash, Version, Redirects, TimeToHeaders, TargetUrl and Elapsed. Elapsed is based on the stopwatch restarted for the final send, not a guaranteed entire-chain duration. A non-null overridable HandleAsync result returns earlier after version normalization; the remaining ordinary metadata assignments are not guaranteed on that branch. Request and response messages are disposed in finally, and caught exceptions become failed responses. [src/LucasSpider/Downloader/HttpClientDownloader.cs:L124–L150](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/HttpClientDownloader.cs#L124-L150), [src/LucasSpider/Http/HttpResponseMessageExtensions.cs:L1–L34](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/HttpResponseMessageExtensions.cs#L1-L34).

Request conversion copies dictionary headers without validation and supports owned string/byte content for DELETE, POST, PATCH and PUT after method uppercasing. Stored/cloned Request.Version is not assigned by ToHttpRequestMessage; the actual wire version is a framework/handler boundary. Content header copying currently addresses httpRequestMessage.Content before the new local content is assigned; a nonempty content-header collection can therefore fail at that access and be converted by the downloader catch. Response failure creation distinguishes timeout exceptions, redirect-message matches, HttpRequestException and other messages into local failure status representations; these are not observed remote HTTP statuses. [src/LucasSpider/Http/Request.cs:L188–L238](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L188-L238), [src/LucasSpider/Http/Response.cs:L153–L177](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Response.cs#L153-L177), [src/LucasSpider/Http/ExtraHttpStatusCode.cs:L1–L10](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/ExtraHttpStatusCode.cs#L1-L10).

Default/proxy handlers configure decompression and certificate callback composition. IgnoreServerCertificateError or its source-supported environment/property gate can install a callback that accepts certificates; this is an explicit configuration-dependent trust boundary. No destination/DNS/egress policy, credential redirect protection, live proxy availability or deployed authentication is established by these methods. URL/request logging call sites and header-dumping utilities require deployment redaction/access review. [src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs:L1–L67](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs#L1-L67), [src/LucasSpider/ServiceCollectionExtensions.cs:L39–L42](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/ServiceCollectionExtensions.cs#L39-L42), [src/LucasSpider/Downloader/HttpClientDownloader.cs:L54–L121](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/HttpClientDownloader.cs#L54-L121), [src/LucasSpider/Http/HeaderUtilities.cs:L1–L30](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/HeaderUtilities.cs#L1-L30).

Confidence is high for owned control flow; HttpClient/handler/provider behavior beyond the inspected calls is an external implementation boundary. See [alternative downloaders](browser-file-download.md), [proxies](../systems/proxy-rotation.md) and [models](../systems/request-response-models.md).

Both owned handler builders return a fresh AdditionalHandlers list on every getter access, so additions made to a previously retrieved list are not retained by Build’s later access. Default Build creates an HttpClientHandler with UseCookies true when no primary handler is supplied, then casts its primary handler to HttpClientHandler to set redirect controls; a different supplied handler type can fail that cast. Proxy Build immediately composes a supplied primary handler with a fresh additional list and skips its owned name/proxy/cookie/decompression/certificate setup. Without a supplied primary it creates ProxyHttpClientHandler with UseCookies true. Cookie/session outcomes and external pipeline behavior remain unknown. [src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs:L1–L67](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs#L1-L67), [src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs:L1–L62](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Proxy/ProxyHttpMessageHandlerBuilder.cs#L1-L62).

A PPPoE match is not a guaranteed BadGateway early response: completed non-null Linux redial process waits fall through to a platform exception, which the parent downloader converts to failure. See [PPPoE branches](browser-file-download.md). [src/LucasSpider/Downloader/PPPoEService.cs:L34–L77](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PPPoEService.cs#L34-L77), [src/LucasSpider/Downloader/PPPoEHttpClientDownloader.cs:L1–L57](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PPPoEHttpClientDownloader.cs#L1-L57), [src/LucasSpider/Downloader/HttpClientDownloader.cs:L124–L150](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/HttpClientDownloader.cs#L124-L150).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
