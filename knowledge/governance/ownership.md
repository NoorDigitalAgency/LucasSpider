---
schema_version: 1
kind: governance
id: lucasspider-ownership
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-10T03:20:42+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Proposed stewardship and review boundary

The crawler supplied zlzforever (56 commits, 61,919 lines, share 0.78) and Sojaner (49 commits, 16,345 lines, share 0.206) as historical contributor candidates. The metadata owner field retains both supplied logins as attribution, not a claim that either currently holds business authority. Requested source reviewer from the saved target is zlzforever. Current membership, availability, review eligibility and delegated authority are unknown at draft time.

No current owner or steward is established by the inspected technical source. `src/LucasSpider/Builder.cs:69–94` and `src/LucasSpider/Spider.cs:234–252` anchor the repository capability under review; they do not prove human ownership. Contribution statistics originate from the crawler target packet, not these source lines. The user reports smortazavi90 has left the organization; historical attribution must never become a current reviewer/steward assignment.

Every record remains proposed. An independently authorized reviewer must establish their authority and assess the pinned evidence before acceptance; this extraction and any agent review are not human acceptance. Source changes, dependency pins, routing/retry semantics, output or authorization boundaries require revalidation. Expiry: until overridden or removed. See [open questions](../decisions/conflicts-and-open-questions.md).

All source citations in this record refer to commit `495ed7cc49208acaa50de7dcf5ebdec584394000`. Observation: 2026-10-10T03:20:42+00:00. Method: static pinned-native-blob comparison, with a payload-scrubbed subset graph for discovery. Freshness: until overridden or removed; any cited-path or relevant pin change requires revalidation. Historical attribution is shared by zlzforever and Sojaner; current accepting steward is unknown.
