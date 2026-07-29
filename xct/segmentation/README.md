# Segmented Classical Tibetan, curated slice (eval'd against SOAS gold)

`xct/segmentation` — silver tier, anchoring: passage-urn. Produced by `nabu data build xct/segmentation` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

Tsheg-bar/word segmentation over a curated Derge slice with the segmenter's error rate measured against the SOAS gold corpus and published in-band — the calibration ground for any full-canon layer.

## Maintenance

re-derive on canonical text revisions or segmenter upgrades; each release republishes the eval number

## Provenance

Canonical inputs at derivation:

- `derge-kangyur` @ `a582cf471b7c85a101035071078032f106a8e536`
- `soas-tibetan` @ `d2b4fbb36a39b6344690168a0aad20472fa22ab725db14ea089304f36429aff8`

Recipe: xct/segmentation v1: curated slice = every live soas-tibetan document (gold segmentation + POS verbatim from Zenodo 574878) + urn:nabu:derge-kangyur:toh21 silver-segmented by a pure-Ruby unigram-cost Viterbi segmenter over tsheg-bar units (closed attached-clitic class འིས/འི/འོ/འང/འམ/ར/ས split only on a known stem, max word span 5 tsheg-bars, unknown pseudo-count 0.05) trained on the SOAS gold token counts alone (external lexica measured unhelpful or harmful in the 2026-07-29 spike and deliberately excluded); eval = leave-one-text-out cross-validation against the SOAS gold, boundary F1 over line-interior token starts, published in the manifest nabu.eval block. Offsets index the passage's NFC text; Passage_SHA256 anchors each row to the exact catalog passage bytes.

Derivation fingerprint: `319b3e1be1400399343dc5b0de208cfa77f60adf0aae96c24757a09172eefcae`.

## The slice — and why it is small

This release is deliberately a CURATED SLICE, not the canon: the four
SOAS gold texts (the eval set itself, published with their gold
segmentation) plus one complete Kangyur text, Toh 21 — Shes rab snying
po (the Heart Sutra) — chosen because it is short (19 passages),
complete, and studied enough that every silver segmentation decision
can actually be reviewed by a human. The segmenter's error rate below
is the calibration number any full-canon layer would have to answer to.

## The eval — the headline number

Boundary F1 **0.9621**
(precision 0.9374,
recall 0.9881; exact-token
F1 0.9094) against
soas-tibetan gold segmentation (Zenodo 574878) — 4 texts,
991 lines, 318230 gold tokens.
Protocol: leave-one-text-out cross-validation. Contamination:
clean — each fold's segmenter is trained only on the other texts' gold counts, never on the text it is scored on. The same numbers ride
`datapackage.json` under `nabu.eval`.

## Columns

`URN` + `Passage_SHA256` are the anchoring contract: rows apply only to
a passage whose Nabu content sha matches. `Position` is the 1-based
token index in the passage; `Offset` the 0-based character offset of
`Form` in the passage's NFC text (the token is always the exact
substring at its offset). `Tier` is `gold` for SOAS rows (segmentation
verbatim from the deposit) and `silver` for segmenter output. Gold POS
tags are NOT columns here — they ride the CoNLL-U projection
(`segmentation.conllu`, XPOS field) so nothing invented ever sits next
to something gold.

## Loading

    import pandas as pd
    df = pd.read_csv("segmentation.csv", keep_default_na=False)
