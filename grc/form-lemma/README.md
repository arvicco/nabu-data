# Ancient Greek form→lemma table from the GLAUx treebanks, with the hand-annotated share counted

`grc/form-lemma` — silver tier, anchoring: none. Produced by `nabu data build grc/form-lemma` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

Maps every lemmatized Ancient Greek word form of the GLAUx corpus (8th c. BC – 4th c. AD, literary and documentary) to its lemma and AGDT 9-place positional tag, with attestation counts, plus a per-lemma sidecar — a corpus-scale form→lemma table spanning a millennium of Greek. SILVER: most of GLAUx is automatic annotation (lemma accuracy ~98.8% per its README), so every row also carries Manual_Count, the attestations from sentences GLAUx marks as hand-annotated, keeping the gold share separable. GLAUx ALONE: the catalog's PROIEL Greek is CC BY-NC-SA and contributes nothing, and GLAUx's own nc texts (NC source texts, PROIEL- and Gorman-annotated trees) are excluded too — both exclusions censused in the manifest. Forms carried verbatim. GLAUx is CC BY-SA → the dataset is CC BY-SA 4.0 (the D51-a share-alike carve-out).

## Maintenance

re-derive after `nabu sync glaux` (upstream releases occasionally; a release that re-runs the automatic annotation shifts silver counts); mechanical, spot-check the Manual_Count share

## Provenance

Canonical inputs at derivation:

- `glaux` @ `b077d8f6ff429a5c7245954bc16bb7d1d7948823`

Recipe: grc/form-lemma v1: sweep the stored token annotations of every live passage of the glaux source ALONE (no other source's Greek — PROIEL is CC BY-NC-SA and contributes nothing) whose document's effective license class is open/attribution (the nc-overridden GLAUx texts — NC source texts, PROIEL- and Gorman-annotated trees — are excluded, censused); keep the tokens bearing a lemma (artificial elliptic nodes and punctuation carry none, censused); carry Form/Lemma/Postag byte-verbatim; count attestations at the distinct (Form, Lemma, Postag) grain into form-lemma.csv and at the Lemma grain into lemmas.csv, each with a Manual_Count of the attestations in sentences GLAUx marks analysis="manual".

Derivation fingerprint: `ff34afbd4131789340f2e951ff05b33b4dfd6185c2b71c6062160c76420e1596`.

## Using this dataset

`form-lemma.csv` maps attested Ancient Greek word forms to their GLAUx lemmas.
Columns: `Form` — the word as the edition writes it (NFC); `Lemma` — the GLAUx
lemma; `Postag` — the AGDT 9-place positional tag verbatim (`n-s---nn-` = noun,
singular, neuter, nominative); `Count` — attestations; `Manual_Count` — the
attestations from hand-annotated sentences. **Most of GLAUx is annotated
automatically** (lemma accuracy ~98.8% per the GLAUx README), so `Count` is a
silver figure; keep `Manual_Count > 0` for the hand-verified share. `lemmas.csv`
re-buckets the same tokens per `Lemma`. Texts whose source or manual annotation is
non-commercial (PROIEL, Gorman trees) are excluded (counts in `datapackage.json` →
`nabu.eval`).

Load with pandas:

    df = pd.read_csv("form-lemma.csv", dtype=str).astype({"Count": int, "Manual_Count": int})
    gold = df[df.Manual_Count > 0]

How to cite: Keersmaekers (2021), doi:10.18653/v1/2021.lchange-1.6 (the `glaux` key
in `sources.bib`; GLAUx data CC BY-SA) — alongside this dataset's `datapackage.json`
provenance block.
