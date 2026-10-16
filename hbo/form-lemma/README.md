# Biblical Hebrew form→lemma table derived from the Open Scriptures Hebrew Bible

`hbo/form-lemma` — gold-derived tier, anchoring: none. Produced by `nabu data build hbo/form-lemma` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

Maps every attested Biblical Hebrew word form of the Westminster Leningrad Codex to its OSHB lemma — the augmented Strong's id verbatim (prefix morphemes slash-joined, homograph letters kept), its content head lemma, and the OSHM morphology code — with attestation counts, plus a per-head-lemma sidecar. OSHB ALONE: the catalog's BHSA Hebrew is CC BY-NC and contributes nothing (the exclusion is censused in the manifest); Aramaic words and qere readings are excluded and censused too. Forms are carried byte-verbatim and never NFC-normalized — hbo is NFC-exempt (the Masoretic mark order is not NFC-stable). OSHB's lemma/morphology layer is CC BY 4.0 over the public-domain WLC text → clean CC BY 4.0.

## Maintenance

re-derive after `nabu sync oshb` (upstream is a completed digitization with occasional corrections); mechanical, no review needed beyond spot-checks

## Provenance

Canonical inputs at derivation:

- `oshb` @ `3d15126fb1ef74867fc1434be1942e837932691f`

Recipe: hbo/form-lemma v1: sweep the stored token annotations of every live passage of the oshb source ALONE (no other source's Hebrew — BHSA is CC BY-NC and contributes nothing); keep the running-text tokens bearing a lemma whose OSHM language prefix is Hebrew — Aramaic tokens and the qere apparatus readings mint no row, both censused; carry Form/Lemma/Morph byte-verbatim (hbo is NFC-exempt, never re-normalized); count attestations at the distinct (Form, Lemma, Morph) grain into form-lemma.csv and at the Head_Lemma (final "/" segment of the augmented Strong's lemma) grain into lemmas.csv.

Derivation fingerprint: `c49d001443714aac8c98c23a59524bbd8e988a863b1eae5f26761864450f64b2`.

## Using this dataset

`form-lemma.csv` maps attested Biblical Hebrew word forms to their OSHB lemmas.
Columns: `Form` — the pointed word as the Westminster Leningrad Codex writes it
(OSHB's `/` morpheme divider removed; bytes verbatim — **never NFC-normalize**,
the Masoretic mark order is not NFC-stable); `Lemma` — OSHB's augmented Strong's
lemma verbatim (prefix morphemes slash-joined, homograph letters suffixed:
`c/d/776`, `1254 a`); `Head_Lemma` — its final segment, the content lemma;
`Morph` — the OSHM morphology code verbatim; `Count` — attestations.
`lemmas.csv` re-buckets the same tokens per `Head_Lemma`. Aramaic words and qere
readings are excluded (counts in `datapackage.json` → `nabu.eval`).

Load with pandas:

    df = pd.read_csv("form-lemma.csv", dtype=str).astype({"Count": int})

How to cite: credit the Open Scriptures Hebrew Bible Project,
https://github.com/openscriptures/morphhb (lemma/morphology CC BY 4.0; the `oshb`
key in `sources.bib`) — alongside this dataset's `datapackage.json` provenance block.
