# Gold lemma frequencies per language at century grain (the diachronic frequency tables)

`mul/lemma-frequencies` — gold-derived tier, anchoring: none. Produced by `nabu data build mul/lemma-frequencies` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

How often does a word occur in a premodern language, and how did that change over the centuries? Frequency dictionaries exist for almost none of the ancient and premodern languages, and diachronic ones for none. This dataset publishes Nabu's lemma census built from human-verified (gold) lemmatization only: for each lemma, language, century and corpus, how many passages and documents attest it — Sanskrit, Sumerian, Middle High German, Middle Dutch, Hebrew, Egyptian, Latin, Akkadian, Greek, Old East Slavic, Classical Chinese, Old Norse, Coptic and dozens more. Teaching tools get real core vocabularies; historical linguists get the rise and fall of words at century grain.

Frequency tables for the ancient and premodern languages at century grain — frequency dictionaries exist for almost none of these languages, diachronic ones for none. One row per (lemma, language, century, basis, corpus) with passage attestations and attesting documents, projected from the catalog's lemma rollup; the lemma is the folded lookup key, the century the signed index of the document's date-envelope midpoint, undated material in its own row. Scope: GOLD lemmatization only (treebank / verified annotation) — the silver grade is skipped and censused, and silver-estimate datings fold into undated (an estimate is never published). License screening row-by-row: open+attribution classes only — nc, ODbL and research_private sources are excluded and censused (rows and occurrences per class) in nabu.eval, so no screened contribution can hide in an integer; CC BY-SA 4.0 — the share-alike carve-out carrying the share-alike lanes (aes, tla-hf, menota, glaux, ...).

## Maintenance

re-derive after lemma-moving events (sync waves of treebank/annotated sources, a rebuild or builders:refresh re-projecting the rollup); the published-slice digest makes an unchanged slice a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: lemma-frequencies v1: project lemma_rollup grade gold at (lemma, language, century, basis, source) grain, silver-estimate datings folded undated, license classes open+attribution only, ordered (language, lemma, century, basis, source); published-slice sha256=c99293b257ee77aadd542b34e234612c5a9dbe3312a118299faa042fcd538d21

Derivation fingerprint: `9bc33f1692fde4732f877ab281b254b1ebe0bdfac9ee619203dd101d43016ff6`.
