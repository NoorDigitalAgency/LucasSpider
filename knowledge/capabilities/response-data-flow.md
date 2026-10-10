---
schema_version: 1
kind: capability
id: lucasspider-response-data-flow
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
  path: src/LucasSpider/DataFlow/Parser/DataParser.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/DataFlowContext.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/JsonFileStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/FileStorageBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Response parsing, follow requests and file output

For a matched successful response, Spider creates a service scope and DataFlowContext, awaits registered data flows in order, then submits FollowRequests and records success. A data-flow exception records scheduler failure and attempts re-enqueue; context disposal runs finally. Evidence: `src/LucasSpider/Spider.cs:308–327,363–404`.

DataParser validates the current request, creates a selectable when needed, calls the subclass ParseAsync, evaluates follow-request queries, validates the resulting requests, copies Owner and Agent, and adds them to the context. Selectable construction has HTML, JSON, XML and text branches; selector implementations were not inspected. Evidence: `src/LucasSpider/DataFlow/Parser/DataParser.cs:126–190`. Selector-based follow queries obtain links and create new requests via the context; AddParsedResult stores or extends typed results. Evidence: `src/LucasSpider/DataFlow/Parser/DataParser.cs:46–60,81–100`.

DataFlowContext holds request, response, options, service provider, follow requests and a data dictionary. Its GetData() returns an immutable dictionary snapshot; stored values remain shallow references. Evidence: `src/LucasSpider/DataFlow/DataFlowContext.cs:14–62,147–176`.

The inspected JsonFileStorage writes serialized context data using WriteLineAsync to a file under the owner-specific data folder. FileStorageBase creates a folder beneath the application base directory and opens output with File.OpenWrite. Evidence: `src/LucasSpider/DataFlow/Storage/JsonFileStorage.cs:22–35`, `src/LucasSpider/DataFlow/Storage/FileStorageBase.cs:20–55`. Do not infer append-only history, atomic commits, cross-process write safety, retention or successful database persistence from this path.

Confidence: high for static sequencing and inspected file-output implementation. Parsed record schemas, customer data, actual output contents and the selected deployment storage are unknown. Related: [frontier](request-frontier.md), [terms](../vocabulary/crawl-terms.md).

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
