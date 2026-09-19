# Han character × corpus doc-frequency census (the graded-reading substrate)

`mul/char-postings` — gold-derived tier, anchoring: none. Produced by `nabu data build mul/char-postings` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

Which Han characters actually occur in premodern East Asian corpora, and how widely? This dataset publishes Nabu's precomputed census: for each character and each corpus, the number of documents attesting it — across Classical Chinese, Japanese, Old Tibetan and Old Japanese collections. Teaching tools can grade reading material by real attestation instead of modern frequency lists; NLP pipelines get historical out-of-vocabulary planning; font projects get honest subsetting data.

Publishes the char_postings census behind Nabu's Han cards and graded-reading lane — one row per (character, corpus) with the attesting document count, spanning lzh/jpn/otb/ojp collections (hence mul/ — the naming the survey left TBD, settled here). The Edubba P-1 rider's character half: frequency data any school can consume, derived from Nabu's ingested corpora only (Edubba's own TSVs are NEVER an input — the circularity guard). nc slices (cbeta, ud, e84000, openiti) excluded row-by-row, censused; CC BY-SA 4.0 — the kanripo lane's share-alike grant (№R-24).

## Maintenance

re-derive after CJK-lane syncs (the census rebuilds with the fulltext index); the published-slice digest makes an unchanged census a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: char-postings v1: project the fulltext char_postings census at (source, character) grain, license classes open+attribution only, ordered (source, codepoint); published-slice sha256=4e9c2ac0f60e06a305092c7a6f0a5424c14f2bc6daee603ce65cd3810c793bee

Derivation fingerprint: `d9b1b2693bb1456aca9d283a016ce8645e055575a1fdca7042d2bf0ed7d3b9ca`.
