# Egyptian hieroglyph frequencies — Gardiner codes censused from AES, per subcorpus

`egy/hiero-frequency` — gold-derived tier, anchoring: none. Produced by `nabu data build egy/hiero-frequency` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

How often does each Egyptian hieroglyph actually occur in real texts — and in which genres? This dataset censuses Gardiner-code frequencies from the Ancient Egyptian Sentences corpus (TLA gold annotation): for every sign, its token occurrences and attesting document counts, overall and per subcorpus (Pyramid Texts, Amarna letters, medical papyri…). Sign-learning curricula can order signs by real attestation instead of list order; join to egy/unikemet-signs by the Gardiner column for identities.

The sign-learning survey's P-1 Egyptian half (P77-r17): Gardiner-code token and document frequencies censused from AES's per-word hiero_inventar annotations, overall and per subcorpus (frequency is genre-dependent — Pyramid Texts vs Amarna letters vs medical papyri). To the survey's knowledge the first public hieroglyph frequency list anywhere. Joins egy/unikemet-signs on the Gardiner column. CC BY-SA 4.0 — derived from AES's share-alike grant, the №R-24/D51-a carve-out (the char-postings precedent).

## Maintenance

re-derive after `nabu sync aes`; the doc-attestation digest in the recipe makes an unchanged census a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: hiero-frequency v1: census Gardiner codes from aes hiero_inventar annotations at (code, subcorpus) grain, token + attesting-doc counts, `all` roll-up per code, live rows only; doc-attestation sha256=cb1fce54622a03235f1e70565efe3618625805995f912004f15b11cbaaeab2b0

Derivation fingerprint: `9d8ffb14f9ae9d9b9e6bf50b301b5f6a9252801e863e4060ea9f53060366bf92`.
