---
schema_version: 1
kind: capability
id: lucasspider-http-download
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-10T03:20:42+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Downloader/HttpClientDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/DownloaderOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# HTTP download and redirect metadata

AgentService handles a Request by calling its injected downloader, assigns response.Agent, and publishes the response using the request Owner as routing input. Evidence: `src/LucasSpider/Agent/AgentService.cs:146–170`.

HttpClientDownloader constructs an HttpRequestMessage, creates a client, sends it with ResponseHeadersRead, and follows status codes 301 through 308 when a Location is present, up to MaximumAllowedRedirects. It creates a failed response when that limit is exceeded. Source default MaximumAllowedRedirects is 5. Evidence: `src/LucasSpider/Downloader/HttpClientDownloader.cs:36–108,154–158`, `src/LucasSpider/Downloader/DownloaderOptions.cs:15`.

The ordinary conversion path sets response RequestHash, Version, Redirects, TimeToHeaders, TargetUrl and Elapsed. A non-null result from the overridable HandleAsync returns earlier after version normalization; these assignments are not guaranteed for overrides. Exceptions become failed responses and request/response message collections are disposed in finally. Evidence: `src/LucasSpider/Downloader/HttpClientDownloader.cs:113–151,188–191`.

Client creation obtains a proxy when configured, otherwise uses the request host for the named client, sets timeout from Request.Timeout, and applies an explicit UserAgent. Request conversion copies supplied headers and supports the inspected string/byte content branches. Evidence: `src/LucasSpider/Downloader/HttpClientDownloader.cs:160–185`, `src/LucasSpider/Http/Request.cs:188–238`.

Confidence: high for this HTTP implementation. DNS/network policy, destination allowlists, credential forwarding across redirects, browser downloader behavior, actual HTTP success, and consumer authorization remain unverified. This capability causes outbound network activity when invoked; it is not a proposed read-only MCP operation. URL logging paths exist: `src/LucasSpider/Downloader/HttpClientDownloader.cs:54–65,98–110`. Related: [queue](../systems/message-queue.md), [terms](../vocabulary/crawl-terms.md).

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
