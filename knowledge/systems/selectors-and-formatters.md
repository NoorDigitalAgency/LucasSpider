---
schema_version: 1
kind: system
id: lucasspider-selectors-and-formatters
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
  path: src/LucasSpider/DataFlow/Parser/Formatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/CharacterCaseFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/CutoutFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/DigitUnitFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/DisplaceFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/Download.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/HtmlDecodeFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/RegexAppendFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/RegexFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/RegexReplaceFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/ReplaceFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/SplitFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/StringFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/TimeStampFormater.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/TrimFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/UrlDecodeFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/Formatters/UrlEncodeFormatter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Parser/SelectorExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/Either.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/ExtensionMethods.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/HtmlNodeExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/HtmlNodeOps.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/HtmlNodeSelection.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/IElementOps.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/ISelectorGenerator.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/LRUCache.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/NamespacePrefix.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/Parser.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/Reader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/Selector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/SelectorGenerator.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/Token.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/TokenKind.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/HtmlAgilityPack.Css/Tokener.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/HtmlUtilities.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/CssSelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/HtmlSelectable.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/ISelectable.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/ISelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/JsonPathSelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/JsonSelectable.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/NotSelectable.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/RegexSelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/Selectable.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/SelectableType.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/SelectorType.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/Selectors.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/TextSelectable.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/XPathSelector.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Selector/XmlSelectable.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Selectable adapters, selector caches and formatter contracts

Selectable exposes selector-based single/list extraction and links/nodes/value/clone adapters. HTML normalizes relative href/src values against the supplied base and optionally removes links by regex domain matching; this rewriting is not an egress authorization check. CSS and XPath parse HTML and return node/text/NotSelectable representations; missing-list results can be null. JSONPath parses with Json.NET and selects tokens, regex applies its replacement to matches, and malformed input/expressions can throw. JSON and XML Links throw NotImplementedException; NotSelectable operations also throw rather than behaving as empty enumerable adapters. [src/LucasSpider/Selector/Selectable.cs:L1–L82](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/Selectable.cs#L1-L82), [src/LucasSpider/Selector/HtmlSelectable.cs:L1–L110](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/HtmlSelectable.cs#L1-L110), [src/LucasSpider/Selector/CssSelector.cs:L1–L109](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/CssSelector.cs#L1-L109), [src/LucasSpider/Selector/XPathSelector.cs:L1–L112](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/XPathSelector.cs#L1-L112), [src/LucasSpider/Selector/JsonPathSelector.cs:L1–L68](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/JsonPathSelector.cs#L1-L68), [src/LucasSpider/Selector/RegexSelector.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/RegexSelector.cs#L1-L78), [src/LucasSpider/Selector/JsonSelectable.cs:L1–L58](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/JsonSelectable.cs#L1-L58), [src/LucasSpider/Selector/XmlSelectable.cs:L1–L60](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/XmlSelectable.cs#L1-L60), [src/LucasSpider/Selector/NotSelectable.cs:L1–L57](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/NotSelectable.cs#L1-L57), [src/LucasSpider/Selector/TextSelectable.cs:L1–L96](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/TextSelectable.cs#L1-L96), [src/LucasSpider/Infrastructure/HtmlUtilities.cs:L1–L70](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/HtmlUtilities.cs#L1-L70).

Selectors caches constructed selector instances in a static concurrent dictionary using source-defined keys; there is no eviction in that factory. The integrated tracked CSS component has its own tokenizer, reader, parser, selector generator and HtmlNodeOps execution pipeline. It handles grouped selectors, combinators, attribute predicates, supported pseudo functions and registered custom delegates; unsupported/malformed forms throw. Numeric nth parsing accepts an integer position through the implemented branch, not arbitrary CSS arithmetic. No external component implementation or origin repository was inspected. [src/LucasSpider/Selector/Selectors.cs:L1–L82](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Selector/Selectors.cs#L1-L82), [src/LucasSpider/HtmlAgilityPack.Css/Tokener.cs:L1–L313](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/HtmlAgilityPack.Css/Tokener.cs#L1-L313), [src/LucasSpider/HtmlAgilityPack.Css/Reader.cs:L1–L156](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/HtmlAgilityPack.Css/Reader.cs#L1-L156), [src/LucasSpider/HtmlAgilityPack.Css/Parser.cs:L1–L646](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/HtmlAgilityPack.Css/Parser.cs#L1-L646), [src/LucasSpider/HtmlAgilityPack.Css/SelectorGenerator.cs:L1–L277](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/HtmlAgilityPack.Css/SelectorGenerator.cs#L1-L277), [src/LucasSpider/HtmlAgilityPack.Css/HtmlNodeOps.cs:L1–L415](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/HtmlAgilityPack.Css/HtmlNodeOps.cs#L1-L415).

HtmlNodeSelection compiles selectors through the owned parser and an adjustable LruCache; single selection takes the first result. LruCache evaluates a miss outside its lock and updates data/list state inside locks, so it is not a single-flight evaluator. Its overflow and capacity-shrink branches call Remove, which already removes the linked-list entry, then RemoveFirst again: more than the intended entry can be removed, and an empty list can fail. Dispose is empty. These source branches qualify any claim of a correct bounded cache; no load/concurrency test was run. [src/LucasSpider/HtmlAgilityPack.Css/HtmlNodeSelection.cs:L1–L98](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/HtmlAgilityPack.Css/HtmlNodeSelection.cs#L1-L98), [src/LucasSpider/HtmlAgilityPack.Css/LRUCache.cs:L1–L132](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/HtmlAgilityPack.Css/LRUCache.cs#L1-L132).

Formatter.Format always calls CheckArguments, uses Default for a default/null input, otherwise calls Handle. Owned formatters cover case/trim/split/cutout/displacement, literal/regex replacement or append/match, format strings, HTML/URL encoding and numeric/time conversion. Checks vary: Split validates its separator/index, regex/format-string variants require arguments, while several other checks are empty. Missing delimiters, empty split results, invalid regex/group/encoding/format or conversion may throw; the parser’s double-call behavior affects these transformations and side effects. [src/LucasSpider/DataFlow/Parser/Formatter.cs:L1–L53](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatter.cs#L1-L53), [src/LucasSpider/DataFlow/Parser/Formatters/SplitFormatter.cs:L1–L55](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/SplitFormatter.cs#L1-L55), [src/LucasSpider/DataFlow/Parser/Formatters/CutoutFormatter.cs:L1–L69](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/CutoutFormatter.cs#L1-L69), [src/LucasSpider/DataFlow/Parser/Formatters/RegexFormatter.cs:L1–L68](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/RegexFormatter.cs#L1-L68), [src/LucasSpider/DataFlow/Parser/Formatters/RegexAppendFormatter.cs:L1–L49](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/RegexAppendFormatter.cs#L1-L49), [src/LucasSpider/DataFlow/Parser/Formatters/RegexReplaceFormatter.cs:L1–L43](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/RegexReplaceFormatter.cs#L1-L43), [src/LucasSpider/DataFlow/Parser/Formatters/StringFormatter.cs:L1–L37](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/StringFormatter.cs#L1-L37), [src/LucasSpider/DataFlow/Parser/Formatters/UrlEncodeFormatter.cs:L1–L49](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/UrlEncodeFormatter.cs#L1-L49), [src/LucasSpider/DataFlow/Parser/DataParser`.cs:L200–L222](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/DataParser%60.cs#L200-L222).

DigitUnitFormatter parses a matched decimal, branches on its unit constants and contains a repeated UnitStringForBai condition; intended coverage should not be inferred from the class name. TimeStampFormatter chooses seconds/milliseconds from source-supported input lengths, converts to local time and rejects unsupported lengths. Download is a network/file side-effect formatter: its WebClient.DownloadFile arguments pass the derived output file as the address and original value as the destination, the reverse of the apparent intent. It is not a verified safe download transformation. Runtime values, network destinations and actual files were not accessed. [src/LucasSpider/DataFlow/Parser/Formatters/DigitUnitFormatter.cs:L1–L67](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/DigitUnitFormatter.cs#L1-L67), [src/LucasSpider/DataFlow/Parser/Formatters/TimeStampFormater.cs:L1–L52](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/TimeStampFormater.cs#L1-L52), [src/LucasSpider/DataFlow/Parser/Formatters/Download.cs:L1–L34](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Parser/Formatters/Download.cs#L1-L34).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
