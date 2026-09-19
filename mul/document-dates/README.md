# Normalized document datings across the multilingual catalog, verbatim raw in-band

`mul/document-dates` — gold-derived tier, anchoring: document-urn. Produced by `nabu data build mul/document-dates` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

When was each ancient document written? This dataset publishes Nabu's normalized answer across its whole multilingual catalog: for each dated document (cited by its stable URN), the year span the corpus's own dating resolves to — signed years, negative for BCE — together with the verbatim upstream dating string it was derived from, so every normalization can be checked against its source. Time-series and period-stratified corpus work gets one uniform dating table instead of a dozen per-corpus conventions.

Publishes the dating layer behind Nabu's timeline — ~700K dated documents as normalized signed year spans (negative = BCE) with the VERBATIM upstream dating string riding every row, so each normalization is checkable against its source. License classes open+attribution only — the nc slices AND the rundata ODbL lane (a copyleft class of its own) are excluded row-by-row, censused in nabu.eval; CC BY-SA 4.0 — the №R-24 carve-out carrying the share-alike lanes (edh, tla-hf, aes, ...).

## Maintenance

re-derive after dating-moving events (sync waves, infer-dates rule changes — the №R-28 regnal upgrade lands here on its next build); the published-slice digest makes an unchanged projection a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: document-dates v1: project dated document_axes rows at URN grain, license classes open+attribution only, ordered (urn, axis row); published-slice sha256=f6499bcb447d00fd87e329563f7225aa598fc3c250dbb88307942160576c672b

Derivation fingerprint: `7f8873308e7c35eb7263da6140d147d5d5bc35a904b4dc55e5560629b5efa49e`.
