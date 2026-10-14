---
schema_version: 1
kind: system
id: lucasspider-request-response-models
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-14T02:05:11.715079+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/ExitException.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/ByteArrayContentExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/EnumerableExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/HttpStatusCodeExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/LoggerExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/StringExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Extensions/UriExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/ByteArrayContent.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/ContentHeaders.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/EncodingUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/ExtraHttpStatusCode.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/HeaderNames.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/HeaderUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/HttpResponseMessageExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/IHttpContent.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/RedirectResponse.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/RequestHeaders.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/RequestPolicy.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Response.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/ResponseHeaders.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/ResponseReasonPhraseConstants.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/StringContent.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/Check.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/Consts.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/DateTimeHelper.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/DefaultHttpMessageHandlerBuilder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/MySqlFileType.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/ObjectId.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/ObjectUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/PagedResult.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/ParallelUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/SpiderId.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/UriUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/SpiderException.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Request/response values, headers, cloning and utility boundaries

Request carries routing Hash/Owner/Agent/Downloader/Policy, timeout, URI/method/version, retry/depth/speed/timestamp, content and arbitrary Properties. Construction validates method and supported absolute schemes but can retain absent/relative URI until a later consumer requires AbsoluteUri/Host. The RequestUri setter itself simply assigns. Content accepts null or IHttpContent. Clone copies routing/scalars, clones content and copies header/property dictionary entries; arbitrary property values remain shared. PPPoERegex is a technical property entry, not a separate credential store. [src/LucasSpider/Http/Request.cs:L1–L331](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L1-L331), [src/LucasSpider/Http/RequestPolicy.cs:L1–L15](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/RequestPolicy.cs#L1-L15), [src/LucasSpider/Infrastructure/UriUtilities.cs:L1–L53](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/UriUtilities.cs#L1-L53).

RequestHeaders, ResponseHeaders and ContentHeaders wrap mutable dynamic dictionaries with named conveniences; they do not provide general canonicalization or typed validation of externally supplied values. RequestHeaders.IfModifiedSince and ResponseHeaders.TransferEncodingChunked are standalone auto-properties rather than dictionary-backed accessors, and Request.Clone copies only the dictionary header entries. ToResponseAsync joins header values, buffers body bytes and copies status/reason/version; it does not populate every richer response field or trailing-header representation. [src/LucasSpider/Http/RequestHeaders.cs:L1–L176](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/RequestHeaders.cs#L1-L176), [src/LucasSpider/Http/ResponseHeaders.cs:L1–L126](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/ResponseHeaders.cs#L1-L126), [src/LucasSpider/Http/ContentHeaders.cs:L1–L81](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/ContentHeaders.cs#L1-L81), [src/LucasSpider/Http/HttpResponseMessageExtensions.cs:L1–L34](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/HttpResponseMessageExtensions.cs#L1-L34), [src/LucasSpider/Http/Request.cs:L258–L288](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L258-L288).

Response contains status/reason, body, version, Agent/RequestHash, target, redirects and elapsed/header timing. Its success predicate covers the source 2xx range; EnsureSuccessStatusCode throws otherwise. Failure factories create local connection/timeout/redirect representations. Clone copies bytes/headers and clones Redirects, but assumes a non-null redirect list; failed/placeholder responses need not initialize that list. Disposal clears headers and body. StringContent.Dispose dereferences its optional header dictionary without a guard, unlike ByteArrayContent; context disposal uses helpers that catch disposal exceptions. [src/LucasSpider/Http/Response.cs:L1–L213](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Response.cs#L1-L213), [src/LucasSpider/Http/RedirectResponse.cs:L1–L42](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/RedirectResponse.cs#L1-L42), [src/LucasSpider/Http/StringContent.cs:L1–L72](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/StringContent.cs#L1-L72), [src/LucasSpider/Http/ByteArrayContent.cs:L1–L66](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/ByteArrayContent.cs#L1-L66), [src/LucasSpider/Infrastructure/ObjectUtilities.cs:L1–L57](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/ObjectUtilities.cs#L1-L57).

Body decoding tries content-type charset, HTML meta charset, byte-order mark and UTF-8 fallback in that order. IsTextData checks strict UTF-8 decode and a source-defined control-character ratio; media-type helpers and HTML detection then guide parser selection. Supported charset names/byte markers are technical decoding policy, not observed payload encoding. Invalid/empty/null body states can fail at consumers rather than being normalized everywhere. [src/LucasSpider/Http/EncodingUtilities.cs:L1–L130](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/EncodingUtilities.cs#L1-L130), [src/LucasSpider/Extensions/ByteArrayContentExtensions.cs:L1–L79](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/ByteArrayContentExtensions.cs#L1-L79), [src/LucasSpider/Extensions/StringExtensions.cs:L1–L71](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Extensions/StringExtensions.cs#L1-L71).

ObjectId generates timestamp/random/increment-based identifiers, validates/parses its byte/hex representations, compares components and supports only its implemented conversions; it is not a cryptographic authorization token. SpiderId requires nonblank bounded ID and falls back Name to ID. DateTimeHelper derives local calendar values. Check provides argument guards; ParallelUtilities builds ActionBlock work, completes it and synchronously waits, with caller-provided execution options. None of these helpers establishes tenant/resource permission or a bound for the crawler’s separate spawned work. [src/LucasSpider/Infrastructure/ObjectId.cs:L1–L747](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/ObjectId.cs#L1-L747), [src/LucasSpider/Infrastructure/SpiderId.cs:L1–L27](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/SpiderId.cs#L1-L27), [src/LucasSpider/Infrastructure/DateTimeHelper.cs:L1–L84](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DateTimeHelper.cs#L1-L84), [src/LucasSpider/Infrastructure/Check.cs:L1–L68](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/Check.cs#L1-L68), [src/LucasSpider/Infrastructure/ParallelUtilities.cs:L1–L44](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/ParallelUtilities.cs#L1-L44).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
