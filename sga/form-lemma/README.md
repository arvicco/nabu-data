# Old Irish form→lemma table from two gold editions of the St Gall Priscian glosses

`sga/form-lemma` — gold-derived tier, anchoring: none. Produced by `nabu data build sga/form-lemma` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

Bridges attested Old Irish forms to their dictionary lemmas from two independent gold annotations of the same St Gall Priscian glosses — the St Gall Priscian Glosses edition v2.1 (Hofman, Moran, Bauer) and CorPH's St Gall text (ChronHib), both MIT — with Edition, homonym index, part of speech and morphological analysis per row. The differentiator is the two-edition agreement census: the editions are joined on the Thesaurus Palaeohibernicus reference, their tokens aligned by folded form, and identical / fold-equal / divergent lemma counts published in nabu.eval, with every divergent pair side by side in divergences.csv — an inter-annotator measurement and a concordance between two lemmatization conventions no single edition can offer.

## Maintenance

re-derive after a stgall-priscian or corph sync (both upstreams are stable — corph is pinned; the stale-ingest guard enforces freshness); mechanical, every build re-measures the agreement census

## Provenance

Canonical inputs at derivation:

- `corph` @ `e7ef75d5f9a6ea97210f028b7389fa9539fbe8c0`
- `stgall-priscian` @ `fdb2502e7ef97c4cd09ac25511271d1548759fc1`

Recipe: sga/form-lemma v1: sweep the stored gold token annotations of every live stgall-priscian passage and of CorPH's St Gall text (document 0007) in the catalog; keep the lemma-bearing Old Irish tokens (every St Gall analysis; CorPH tokens whose LEMMATA language is Early Irish); count attestations at the distinct (Edition, Form, Lemma, Homonym, Part_Of_Speech, Analysis) grain into form-lemma.csv. Agreement census: join the editions on the Thesaurus Palaeohibernicus reference (St Gall annotations thesaurus; CorPH locus 1 minus the Sg siglum; zero padding dropped on both sides), pool tokens per ref, align greedily in edition order by folded form (NFD, marks stripped, lower-cased, letters only), compare lemmas as identical / equal folded / divergent; census into nabu.eval, divergent pairs into divergences.csv.

Derivation fingerprint: `6e4664dc4d580514bbe9fc26cbad1a6ad3a85c2e7f4ff20a6dfb34ddd703782f`.

## Using this dataset

`form-lemma.csv` maps attested Old Irish surface forms to dictionary lemmas, on gold
(human-annotated) evidence only, from two independent editions of the St Gall Priscian
glosses (St Gallen, Stiftsbibliothek 904). Columns: `Edition` — `stgall-priscian` (the St
Gall Priscian Glosses v2.1, Hofman/Moran/Bauer) or `corph` (CorPH's St Gall text, ChronHib);
`Form` — the analysed form verbatim as the edition stores it (St Gall keeps its editorial
marks); `Lemma` — the edition's headword, its homonym index split into `Homonym` (each
edition numbers homonyms its own way); `Part_Of_Speech` — St Gall's word class (CorPH
carries none per token); `Analysis` — the edition's morphological analysis; `Count` — gold
attestations of the tuple. Only Old Irish tokens count (CorPH's Latin and `.i.` analyses
are excluded).

Load with pandas:

    df = pd.read_csv("form-lemma.csv", dtype=str).astype({"Count": int})

## The two-edition agreement census

The editions are joined on the Thesaurus Palaeohibernicus reference (`nabu.eval.join` in
`datapackage.json`). Within each matched reference the editions' tokens are aligned by
folded form; of 15480 aligned token pairs, 10880 carry
identical lemmas, 1691 more agree once length marks, hyphens and
case are folded, and 2909 diverge (agreement rate
0.8121). `divergences.csv` lists every divergent pair side by
side with both passage URNs — mostly the editions' different headword conventions, a
concordance between the two lemmatizations as much as a proofreading list. Unaligned
tokens (different word division, a word only one edition analysed) are counted in
`nabu.eval.tokens`, never guessed at.

How to cite: cite both editions — Rijcklof Hofman, Pádraic Moran, Bernhard Bauer, *St
Gall Priscian Glosses*, version 2.1 (2023), https://www.stgallpriscian.ie (MIT; the
`stgall-priscian` key in `sources.bib`) and *CorPH — Corpus PalaeoHibernicum*
(Chronologicon Hibernicum, Maynooth; MIT; the `corph` key) — alongside this dataset's
`datapackage.json` provenance block.
