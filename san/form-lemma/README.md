# Sanskrit form→lemma table derived from DCS gold annotations

`san/form-lemma` — gold-derived tier, anchoring: none. Produced by `nabu data build san/form-lemma` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

Bridges inflected surface forms (and unsandhied padapāṭha forms) to lemmas using only human-annotated gold data — powers dictionary-headword lookup for query expansion (the successor to Nabu's rule-generated Sanskrit stem variants).

## Maintenance

re-derive after each dcs sync (upstream updates infrequently); mechanical, no review needed beyond spot-checks

## Provenance

Canonical inputs at derivation:

- `dcs` @ `04e0778d3dc971030229179e25eea043d06ff397`

Recipe: san/form-lemma v1: sweep the stored gold token annotations of every live DCS passage in the catalog (annotations_json; the dcs adapter's chapter-info.xml gold gate admits only gold-lexicon chapters, so every token is human-verified); keep exactly the tokens bearing a lemma — lemma-less sandhi-surface lines (CoNLL-U `_`, ~15% of raw token lines upstream) mint no row; read Unsandhied and LemmaId from MISC; count gold attestations at the distinct (Form, Unsandhied, Lemma, Lemma_ID, UPOS) grain into form-lemma.csv and at the (Lemma_ID, Lemma) grain into lemmas.csv.

Derivation fingerprint: `31cb919e257960d99154ca4520f88e75c83196953d4b7fa25029ff26212bccba`.

## Using this dataset

`form-lemma.csv` maps attested surface forms to dictionary lemmas, on gold
(human-verified) evidence only. Columns: `Form` — the surface form as attested
(IAST, sandhi applied); `Unsandhied` — the padapāṭha analysis form (DCS MISC
`Unsandhied`); `Lemma` — the DCS dictionary headword; `Lemma_ID` — DCS's
permanent numeric lemma id, verbatim (the interop key back into DCS);
`Part_Of_Speech` — DCS's UPOS tag; `Count` — gold attestation count.
`lemmas.csv` is the per-lemma sidecar at the (`Lemma_ID`, `Lemma`) grain.

Load with pandas:

    df = pd.read_csv("form-lemma.csv", dtype=str).astype({"Count": int})

How to cite: cite the annotations' source — Oliver Hellwig, *The Digital Corpus
of Sanskrit (DCS)*, 2010–2024, https://github.com/OliverHellwig/sanskrit
(CC BY 4.0; the `dcs` key in `sources.bib`) — alongside this dataset's
`datapackage.json` provenance block.

Derivation note: rows are read from Nabu's catalog — the ingested, gold-gated
DCS chapters, a pure function of `canonical/dcs` — so run `nabu sync dcs`
before building; the recorded cone sha then names exactly the ingested bytes.
