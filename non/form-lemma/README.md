# Old Norse form→lemma table from Menota's lemmatized manuscript transcriptions

`non/form-lemma` — gold-derived tier, anchoring: none. Produced by `nabu data build non/form-lemma` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

Maps every lemmatized word of the Menota archive's Old Icelandic and Old Norwegian manuscripts to its lemma and me:msa morphosyntactic analysis, with attestation counts at each transcription level the word carries — facsimile (the glyphs as written, MUFI characters included), diplomatic (abbreviations expanded, scribal spelling kept) and normalized (standard Old Norse orthography) — the Level column naming which, since dipl-only documents carry lemmatized words with no normalized reading; plus a per-lemma sidecar. A bridge from manuscript spellings to dictionary headwords no single edition offers. Scope is Old Norse as Glottolog bounds it: Old Swedish and Old Danish documents are excluded and censused, as are texts whose own licence is not open. Forms are carried verbatim. Menota is CC BY-SA 4.0 → the dataset is CC BY-SA 4.0 (the D51-a share-alike carve-out).

## Maintenance

re-derive after `nabu sync menota` (the archive grows as editors deposit new transcriptions); mechanical, no review needed beyond spot-checks

## Provenance

Canonical inputs at derivation:

- `menota` @ `5d6201c54bc7d42fab60dc675e2f5db04e074245f11fdd0b39d5c9b31336ded7`

Recipe: non/form-lemma v1: sweep the stored token annotations of every live passage of the menota source ALONE whose document language is Old West Norse (isl, nor, non — swe/dan documents are out of scope, censused) and whose effective license class is open/attribution; keep the <w> tokens bearing a lemma (lemma-less words and punctuation mint nothing, censused); for each level the word attests (facs, dipl, norm) count one attestation at the distinct (Level, Form, Lemma, Msa) grain into form-lemma.csv, carrying every value byte-verbatim (never re-normalized); count each token once at the Lemma grain into lemmas.csv.

Derivation fingerprint: `01656dfc883cf4946b520ebfc159741d035c3a12e89865ee349f03691a52d515`.

## Using this dataset

`form-lemma.csv` maps attested Old Norse word forms — Old Icelandic and Old
Norwegian manuscripts transcribed by Menota — to their lemmas. Columns: `Level` —
the transcription level the form comes from: `facs` (facsimile: the glyphs as
written, MUFI private-use characters and abbreviation marks included — a MUFI font
renders them), `dipl` (diplomatic: abbreviations expanded, the scribe's spelling
kept), `norm` (normalized Old Norse orthography, the dictionary-facing form);
`Form` — the word at that level, verbatim; `Lemma` — Menota's headword; `Msa` — the
`me:msa` morphosyntactic analysis verbatim (`xNC gM nS cN sI`); `Count` —
attestations. One word attested at three levels counts once in each, so filter on
`Level` before summing. `lemmas.csv` counts each lemmatized word once per `Lemma`.
Old Swedish and Old Danish documents are out of scope (counts in
`datapackage.json` → `nabu.eval`).

Load with pandas:

    df = pd.read_csv("form-lemma.csv", dtype=str, keep_default_na=False).astype({"Count": int})
    norm = df[df.Level == "norm"]

How to cite: credit the Medieval Nordic Text Archive, https://www.menota.org, and
the editor(s) named in each text's teiHeader (CC BY-SA 4.0; the `menota` key in
`sources.bib`) — alongside this dataset's `datapackage.json` provenance block.
