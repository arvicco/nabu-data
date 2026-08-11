# Compiled cuneiform sign cards — OSL identity, concordances, attestation counts

`sux/sign-table` — gold-derived tier, anchoring: none. Produced by `nabu data build sux/sign-table` (Nabu 1.4.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

## Why this dataset exists — in plain terms

One reference row per cuneiform sign: its Oracc Sign List identity, Unicode codepoints, the numbers every major printed sign list assigns it, the readings the CDLI convention uses, and — the new part — how many documents of the open cuneiform corpora actually attest it. Sign-list tooling, OCR/HTR training and teaching instruments get identity, concordance and real-world frequency in one table.

The per-sign reference card compiled from what sux/value-signs flattens value-wise: one row per top-level OSL sign with codepoints, every print-list number, the CDLI reading concordance, AND per-source attestation doc-counts over the open cuneiform corpora (cdli/oracc/tlhdig — the Edubba P-1 rider's sign half, true sign-counts at last). Counting scope stated and censused (value/logogram tokens; compounds out); nc lanes (etcsl, ebl) have NO count columns, so no nc contribution can hide in an integer — the lemma_frequencies lesson. Core CC BY 4.0; the Wiktionary/aes BY-SA sense lanes are deliberately deferred to a later sidecar dataset so the core stays BY (survey §2.6).

## Maintenance

re-derive after `nabu sync osl` or cuneiform-lane syncs (counts move with the catalog); the counts digest in the recipe makes an unchanged state a fingerprint no-op

## Provenance

Canonical inputs at derivation:

- `osl` @ `7749a4bd8589491b987ab3da31660ef4abca5012`

Recipe: sign-table v1: one card per top-level OSL sign (identity, codepoints, list numbers, CDLI readings) + per-source attestation doc-counts over cdli/oracc/tlhdig (value/logogram tokens only, distinct-doc grain); counts sha256=0fb2ab8d9c9a99bf947ae82ab3588db5d7de15b823eae5ea4a5e5690f6345c39

Derivation fingerprint: `77f19929f0bc18cf52bd23cab9ca38456059f006e95e101ec0d82b671452696f`.
