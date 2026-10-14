---
schema_version: 1
kind: system
id: lucasspider-build-package-boundaries
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:39.540145+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: .editorconfig
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: .github/workflows/alpha-release.yaml
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: .github/workflows/beta-release.yaml
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: .github/workflows/hotfix-release.yaml
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: .github/workflows/production-release.yaml
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: .github/workflows/publish-job.yaml
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: .github/workflows/pull-request.yaml
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: .github/workflows/test-job.yaml
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: .gitignore
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: LICENSE.txt
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: LucasSpider.sln
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: README.md
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: package.props
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider.Sample/LucasSpider.Sample.csproj
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider.Tests/LucasSpider.Tests.csproj
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Downloader/PuppeteerDownloader.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/LucasSpider.csproj
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/MessageQueue/MessageQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Declared targets, dependencies, CI and publication boundaries

The library declares PackageId LucasSpider and targets netstandard2.1/netstandard2.0; shared package.props sets the latest language version and packaging metadata. Test and sample projects target net8.0 and reference the library. This source does not declare an immutable published implementation identity merely by package name or framework target. The package manifest includes public dependencies such as MessagePack 3.1.4, Microsoft.Playwright 1.57.0, Microsoft.Data.SqlClient 6.1.3, Dapper 2.1.66, HtmlAgilityPack 1.12.4, Microsoft.VisualBasic 10.3.0 and hosting/HTTP 10.0.1; declarations do not establish their implementation or deployment. [src/LucasSpider/LucasSpider.csproj:L1–L31](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/LucasSpider.csproj#L1-L31), [package.props:L1–L22](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/package.props#L1-L22), [src/LucasSpider.Tests/LucasSpider.Tests.csproj:L1–L38](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider.Tests/LucasSpider.Tests.csproj#L1-L38), [src/LucasSpider.Sample/LucasSpider.Sample.csproj:L1–L24](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider.Sample/LucasSpider.Sample.csproj#L1-L24), [LucasSpider.sln:L1–L68](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/LucasSpider.sln#L1-L68).

The pull-request workflow targets develop and invokes the reusable test job. That job selects/checkout references, configures SDK tooling, invokes dotnet test and has a conditional report/tool path. Alpha and hotfix release workflows test before their publish job; beta and production route startup directly to publishing. Publish derives version/stage inputs through referenced actions, packs, then invokes NuGet publication; release jobs create release metadata, with hotfix-specific follow-up. These are source automation controls, not evidence a run passed, a package was published or an action’s external implementation is pinned/inspected. [.github/workflows/pull-request.yaml:L1–L11](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/pull-request.yaml#L1-L11), [.github/workflows/test-job.yaml:L1–L41](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/test-job.yaml#L1-L41), [.github/workflows/alpha-release.yaml:L1–L48](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/alpha-release.yaml#L1-L48), [.github/workflows/beta-release.yaml:L1–L43](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/beta-release.yaml#L1-L43), [.github/workflows/hotfix-release.yaml:L1–L55](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/hotfix-release.yaml#L1-L55), [.github/workflows/production-release.yaml:L1–L43](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/production-release.yaml#L1-L43), [.github/workflows/publish-job.yaml:L1–L41](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/publish-job.yaml#L1-L41).

All tracked paths were classified before blob retrieval. Production code, project/workflow/build metadata, repository documentation, license and ignore/editor configuration were read as technical text. The 13 test and 11 sample C# bodies are whole mixed fixture/sample boundaries; the sample settings, three HTML fixture paths, two JSON datasets and icon image are metadata-only exclusions. Their names/manifests identify test/sample areas, but assertions, sample destinations/configuration, dataset contents and effective test coverage remain unknown. No source tests/builds/operators were executed.

README examples and improvement notes are documentation rather than implementation authority. Redis/distributed/Puppeteer naming in documentation does not supply an inspected broker/scheduler or implemented browser: the owned transport is local, scheduler classes are lists and PuppeteerDownloader is a placeholder. License and editor/ignore conventions do not grant production or knowledge acceptance authority. External workflow actions, package registries and selected consumer implementation relationships remain unknown exact-pin boundaries. [README.md:L1–L215](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/README.md#L1-L215), [LICENSE.txt:L1–L21](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/LICENSE.txt#L1-L21), [.editorconfig:L1–L257](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.editorconfig#L1-L257), [.gitignore:L1–L380](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.gitignore#L1-L380), [src/LucasSpider/MessageQueue/MessageQueue.cs:L1–L73](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/MessageQueue/MessageQueue.cs#L1-L73), [src/LucasSpider/Downloader/PuppeteerDownloader.cs:L1–L32](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Downloader/PuppeteerDownloader.cs#L1-L32).

Release declaration contract (all entrypoints below use workflow_dispatch):

| Entrypoint | reference input | Path to publish | Publish stage | Pack mode |
| --- | --- | --- | --- | --- |
| Alpha | Optional string; empty default | Startup → test → publish | alpha | Debug |
| Beta | Optional string; empty default | Startup → publish | beta | Release |
| Production | Optional string; empty default | Startup → publish | production | Release |
| Hotfix | Required string; no default | Startup → test → publish | production | Release |

The reusable publish workflow uses workflow_call with required string stage and no default. Current callers supply alpha, beta or production, but its input declaration imposes no stage enum. [.github/workflows/alpha-release.yaml:L1–L48](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/alpha-release.yaml#L1-L48), [.github/workflows/beta-release.yaml:L1–L43](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/beta-release.yaml#L1-L43), [.github/workflows/production-release.yaml:L1–L43](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/production-release.yaml#L1-L43), [.github/workflows/hotfix-release.yaml:L1–L55](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/hotfix-release.yaml#L1-L55), [.github/workflows/publish-job.yaml:L1–L41](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/publish-job.yaml#L1-L41).

Publish selects Debug packing for alpha and Release packing for every non-alpha stage. Both pack commands set Version from the analyzed RELEASE_PLAIN_VERSION environment output and include the RepositoryUrl provenance property. The final NuGet push step has no explicit stage condition. These are declared trigger/input/branch/output roles; no workflow, test, pack, release, publication or external action was executed, and successful output, permissions and consumed implementation remain unknown. [.github/workflows/publish-job.yaml:L1–L41](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/.github/workflows/publish-job.yaml#L1-L41).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
