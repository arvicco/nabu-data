# Egyptian hieroglyph frequencies — Gardiner codes censused from AES per subcorpus, with word-grain and damaged-attestation counts

`egy/hiero-frequency` — gold-derived tier, anchoring: none. Produced by `nabu data build egy/hiero-frequency` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

How often does each Egyptian hieroglyph actually occur in real texts — and in which genres? This dataset censuses Gardiner-code frequencies from the Ancient Egyptian Sentences corpus (TLA gold annotation): for every sign, its token occurrences and attesting word and document counts, overall and per subcorpus (Pyramid Texts, Amarna letters, medical papyri…). A companion table, hiero-glyphs.csv, counts each Unicode hieroglyph across the dictionary's per-text hieroglyph transcriptions — texts, occurrences, words, and how many occurrences are damaged (read inside `<unclear>`). Sign-learning curricula can order signs by real attestation instead of list order; join to egy/unikemet-signs by the Gardiner or Codepoint column for identities.

The sign-learning survey's P-1 Egyptian half (P77-r17): Gardiner-code token, word and document frequencies censused from AES's per-word hiero_inventar annotations, overall and per subcorpus (frequency is genre-dependent — Pyramid Texts vs Amarna letters vs medical papyri). To the survey's knowledge the first public hieroglyph frequency list anywhere, now at the word grain: Words counts the words attesting a sign (a sign repeated inside one word counts once). The hiero-glyphs.csv sidecar publishes the AED per-glyph census (the catalog's hiero_postings, over the TLA per-text stand-off hieroglyph files): Texts, Signs, Words, and Unclear — the occurrences read inside TEI `<unclear>`, i.e. damage-flagged attestations. Joins egy/unikemet-signs on the Gardiner column and on Codepoint. CC BY-SA 4.0 — derived from the AES and AED share-alike grants, the D51-a share-alike carve-out of 2026-08-11 (the char-postings precedent).

## Maintenance

re-derive after `nabu sync aes` or `nabu sync aed`; the doc-attestation and glyph-census digests in the recipe make an unchanged census a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: hiero-frequency v2: census Gardiner codes from aes hiero_inventar annotations at (code, subcorpus) grain, token + word (one aes token = one word; a code counts once per word) + attesting-doc counts, `all` roll-up per code, live rows only; doc-attestation sha256=eb759d2d11f4cc78b1bb770d25ad0dab5a78c2ed269560abd8cb8edddd700ea1; plus hiero-glyphs.csv, the catalog's aed hiero_postings per-glyph census verbatim (texts, signs, words, unclear) sha256=72dfa607d2724387527d656b0215046ab3f7f7a51e832b6a6f845d7c594f55e8

Derivation fingerprint: `5020a9a3c0080fb3d60e472208c079b5500a3beeed9ecb03d1e70c9868370f92`.
