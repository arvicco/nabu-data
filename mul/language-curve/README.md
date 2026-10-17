# Documents and passages per language × century × corpus (the attestation census)

`mul/language-curve` — gold-derived tier, anchoring: none. Produced by `nabu data build mul/language-curve` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

When is each ancient and premodern language attested, and how much of it survives from each century? This dataset publishes Nabu's attestation census across its whole multilingual library: for every language, century and corpus, how many documents and passages are held — the rise-and-fall table of the written record, dated by each corpus's own upstream dating. Undated material is counted honestly in its own row.

The library-wide diachronic attestation census — the rise-and-fall table: live documents and passages per (language, century, basis, corpus), projected from the catalog's language curve rollup; the century is the signed index of the document's date-envelope midpoint, undated material in its own row, silver-estimate datings folded into undated. License screening row-by-row: open+attribution classes only — nc, ODbL and research_private sources are excluded and censused (rows and passages per class) in nabu.eval; CC BY-SA 4.0 — the share-alike carve-out.

## Maintenance

re-derive after sync waves, dating-moving events or a rebuild; the published-slice digest makes an unchanged census a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: language-curve v1: project language_curve at (language, century, basis, source) grain, silver-estimate datings folded undated, license classes open+attribution only, ordered (language, century, basis, source); published-slice sha256=26e3f84161f100bded2b852138f47a76ead5b3824155a73ab3d939065b72ed7c

Derivation fingerprint: `6fd25e8692da6e0df7910a840da6a953b7b27a716965b2cfa90dace2cd508856`.
