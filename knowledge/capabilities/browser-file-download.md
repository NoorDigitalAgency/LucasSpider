---
schema_version: 1
kind: capability
id: lucasspider-browser-file-download
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:38.776891+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Downloader/DownloaderOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/Downloaders.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/EmptyDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/FakeHttpClientDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/FileDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/IDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/IProxyDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PPPoEHttpClientDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PPPoEOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PPPoEService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PlaywrightBrowserName.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PlaywrightDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PuppeteerDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/PlaywrightExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/UriUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Browser rendering, file/fake downloaders and PPPoE

UseDownloader inspects public constructors: an IHttpClientFactory parameter adds the owned default HTTP handler builder; an IBrowser parameter adds a singleton Playwright browser selected from Chromium, Firefox or WebKit, then an agent is registered with generated identity. Browser creation blocks on asynchronous factory/launch results in that registration callback. Actual browser installation, launch success and external SDK behavior were not executed or inspected. [src/LucasSpider/Downloader/ServiceCollectionExtensions.cs:L1–L76](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/ServiceCollectionExtensions.cs#L1-L76), [src/LucasSpider/Downloader/DownloaderOptions.cs:L1–L29](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/DownloaderOptions.cs#L1-L29), [src/LucasSpider/Downloader/PlaywrightBrowserName.cs:L1–L12](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PlaywrightBrowserName.cs#L1-L12).

PlaywrightDownloader creates a fresh context with UserAgent and navigation timeout, tracks request callbacks, navigates to RequestUri, waits for NetworkIdle and finds a single final main-frame navigation document. Missing document returns a local failed response; selection/navigation/conversion exceptions are caught and returned as failures. It converts rendered DOM HTML rather than the original wire body, copies response headers, sets correlation/timing/target metadata and conditionally retains redirect history. The request’s method/content/general headers and MaximumAllowedRedirects are not applied by this owned browser method; a Request is therefore not reproduced as a complete HTTP transaction. [src/LucasSpider/Downloader/PlaywrightDownloader.cs:L1–L159](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PlaywrightDownloader.cs#L1-L159).

RenderShadowRoots chooses ContentDeepAsync instead of the normal page-content call. Its embedded script traverses exposed shadowRoot nodes, passes collected roots to documentElement.getHTML, flattens matching shadow templates with nesting accounting and reconstructs document markup with escaped attributes. All seven embedded functions/callbacks were inventoried separately. Closed roots, browser getHTML support, malformed markup and timing remain external/runtime boundaries; there is no iframe traversal guarantee in the owned traversal. [src/LucasSpider/Extensions/PlaywrightExtensions.cs:L1–L74](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/PlaywrightExtensions.cs#L1-L74), [src/LucasSpider/Downloader/PlaywrightDownloader.cs:L140–L154](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PlaywrightDownloader.cs#L140-L154).

PuppeteerDownloader is an owned placeholder returning Gone with synthetic content and RequestHash; it does not launch Puppeteer. FakeHttpClientDownloader overrides SendAsync to return a synthetic OK response while retaining the parent conversion path. EmptyDownloader increments a local count and returns a synthetic OK response. FileDownloader transforms the request URI into a file path and reads bytes synchronously; its NotFound assignment does not return before File.ReadAllBytes, and it has no local catch, so missing/read-protected files can throw instead of returning the intended status. Request URI construction accepts only its supported network schemes for absolute input, so usable file composition is not established by the downloader name alone. [src/LucasSpider/Downloader/PuppeteerDownloader.cs:L1–L32](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PuppeteerDownloader.cs#L1-L32), [src/LucasSpider/Downloader/FakeHttpClientDownloader.cs:L1–L34](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/FakeHttpClientDownloader.cs#L1-L34), [src/LucasSpider/Downloader/EmptyDownloader.cs:L1–L40](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/EmptyDownloader.cs#L1-L40), [src/LucasSpider/Downloader/FileDownloader.cs:L1–L33](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/FileDownloader.cs#L1-L33), [src/LucasSpider/Http/Request.cs:L312–L328](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L312-L328), [src/LucasSpider/Infrastructure/UriUtilities.cs:L1–L53](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/UriUtilities.cs#L1-L53).

PPPoEHttpClientDownloader requires an active PPPoEService, then HandleAsync reads text and applies the request-specific detection regex. A match calls Redial before constructing the early BadGateway response, so that response requires redial to return normally. The Windows branch explicitly returns after redial; the Linux branch returns early if either process start is null, but when both starts and waits complete it falls through to the trailing PlatformNotSupportedException. That exception propagates through HandleAsync into the parent downloader catch and becomes a failed response. Unsupported OS branches also reach that throw. The no-match return is a null Task rather than a completed Task containing null, so awaiting it can likewise fail. The intended early response bypasses ordinary parent metadata assignments. Account/password/interface inputs and process-based termination/redial are source controls only; credentials, processes and networks were never used. [src/LucasSpider/Downloader/PPPoEHttpClientDownloader.cs:L1–L57](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PPPoEHttpClientDownloader.cs#L1-L57), [src/LucasSpider/Downloader/PPPoEService.cs:L1–L131](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PPPoEService.cs#L1-L131), [src/LucasSpider/Downloader/PPPoEOptions.cs:L1–L20](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PPPoEOptions.cs#L1-L20).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
