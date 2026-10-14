---
schema_version: 1
kind: capability
id: lucasspider-entity-extraction
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-14T02:05:11.715079+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/DataParser`.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/EntitySelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/FollowRequestSelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/GlobalValueSelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Model.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Selector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/ValueSelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/DateTimeHelper.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Attribute-driven entity extraction and conversion

DataParser<TEntity>.InitializeAsync creates Model<TEntity>, translates follow selectors for CSS, regex, XPath and JSONPath into follow queriers and accumulates URL patterns as required validators. Environment follow selectors are skipped in this switch. Model reflects class entity/global/follow attributes and public instance properties carrying ValueSelector, attaches formatter attributes and Required markers, and rejects unnamed global selectors. Reflection discovery order and HashSet iteration are not declared a stable user ordering contract. [src/LucasSpider/DataFlow/Parser/DataParser`.cs:L17–L87](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/DataParser%60.cs#L17-L87), [src/LucasSpider/DataFlow/Parser/Model.cs:L1–L110](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Model.cs#L1-L110), [src/LucasSpider/DataFlow/Parser/EntitySelector.cs:L1–L21](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/EntitySelector.cs#L1-L21), [src/LucasSpider/DataFlow/Parser/FollowRequestSelector.cs:L1–L36](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/FollowRequestSelector.cs#L1-L36), [src/LucasSpider/DataFlow/Parser/GlobalValueSelector.cs:L1–L13](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/GlobalValueSelector.cs#L1-L13), [src/LucasSpider/DataFlow/Parser/ValueSelector.cs:L1–L45](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/ValueSelector.cs#L1-L45).

Parsing copies request Properties, overlays global selections, then either parses the whole selectable or selects entity nodes. When a positive Take trims the list, TakeByDescending true takes the first items and false skips to the last items; the name alone must not reverse that branch. An index is passed to each object, non-null configured objects enter the typed result list, and AddParsedResult appends to context data. A missing global selection is dereferenced without the null-safe member access used for ordinary field selection. [src/LucasSpider/DataFlow/Parser/DataParser`.cs:L95–L179](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/DataParser%60.cs#L95-L179).

Each field obtains a selector value or an environment value. Environment cases derive entity index, generated GUID, local date/time/month/week, spider Owner, request Hash, or a property by expression. Nonblank values pass through every formatter. The current loop calls formatter.Format once before its try and a second time inside the try: success can apply transformations twice, and a first-call exception escapes the second-call catch. Afterwards Convert.ChangeType targets the reflected property type, Required null results discard the object, and PropertyInfo.SetValue assigns it. Conversion/setter/configuration failures are not locally caught by ParseObject. [src/LucasSpider/DataFlow/Parser/DataParser`.cs:L182–L299](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/DataParser%60.cs#L182-L299), [src/LucasSpider/DataFlow/Parser/Formatter.cs:L1–L53](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatter.cs#L1-L53), [src/LucasSpider/Infrastructure/DateTimeHelper.cs:L1–L84](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DateTimeHelper.cs#L1-L84).

The attributes describe selected source schema and extraction rules; no customer rows, fixture bodies or downstream entity definitions were read. Required here is a local null-result gate, not a complete validation framework. Nullable/custom conversions, formatter order, malformed selectors and missing globals require caller/source-policy review. Related: [selector contracts](../systems/selectors-and-formatters.md) and [persistence](../systems/entity-storage.md).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
