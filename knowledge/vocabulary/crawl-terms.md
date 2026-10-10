---
schema_version: 1
kind: vocabulary
id: lucasspider-crawl-terms
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-10T03:20:42+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Response.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/DataFlowContext.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestHasher.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Crawl terminology within LucasSpider

| Term | Scoped meaning and evidence | Confidence |
| --- | --- | --- |
| Request | Crawl work description carrying URI, method, content, headers, routing and retry/depth fields; `src/LucasSpider/Http/Request.cs:40–134` | High, source-local |
| Owner | Request field assigned from SpiderId.Id, then used to route responses; `src/LucasSpider/Spider.cs:225`, `src/LucasSpider/Agent/AgentService.cs:157–158` | High, routing identity only |
| Hash / RequestHash | Request hash depends on Owner, absolute URI, Method, RequestedTimes and Content; Response.RequestHash matches pending requests; `src/LucasSpider/Infrastructure/RequestHasher.cs:19–29`, `src/LucasSpider/Spider.cs:308–310` | High, correlation representation, not global URL synonym |
| Agent | Download worker identity copied onto a response and successful matched request; `src/LucasSpider/Agent/AgentService.cs:155`, `src/LucasSpider/Spider.cs:314` | High, source-local |
| FollowRequests | Requests collected while processing a response and returned to scheduler admission; `src/LucasSpider/DataFlow/DataFlowContext.cs:41,65–98`, `src/LucasSpider/Spider.cs:379` | High, source-local |
| DataFlowContext | Per-response request/response/options/services container with parsed data and follow requests; `src/LucasSpider/DataFlow/DataFlowContext.cs:14–62,147–176` | High, source-local |

These are code/domain meanings and representations inside the pinned library. No UI display-label mapping or cross-repository synonym has been established. In particular, Owner does not establish tenant ownership, authenticated caller identity or permission to crawl. Related: [frontier](../capabilities/request-frontier.md), [data flow](../capabilities/response-data-flow.md).

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
