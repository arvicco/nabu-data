# ACTib ↔ Derge Kangyur anchor table (stable anchors for the segmented eKangyur)

`xct/actib-anchors` — gold-derived tier, anchoring: urn+sha. Produced by `nabu data build xct/actib-anchors` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

## Why this dataset exists — in plain terms

The Kangyur is the Tibetan Buddhist canon — in its Derge edition,
over 460,000 lines of text. ACTib (the Annotated Corpus of Classical
Tibetan, by Meelen, Hill & Faggionato) is a widely used scholarly
resource that took a digital copy of that canon and, by computer,
split every line into words and tagged each word's grammar. That
work is genuinely valuable: Classical Tibetan is written without
spaces between words, so a pre-segmented, grammar-tagged canon saves
every researcher months of preparatory work.

But ACTib has one structural flaw: its lines carry no address back
into a citable edition of the text. Each annotated line knows which
scanned volume and page it came from — not which passage of the
canon it annotates, and not what the wording of that passage was at
the moment of annotation. The digital canon it was built from has
been corrected and re-released since, and each time that happens
there is no reliable way to tell whether an ACTib line still matches
the text it describes. Left alone, 460,000 lines of annotation
slowly drift away from the text they annotate — orphaned
scholarship.

This dataset is the missing address book. For every passage of the
Derge Kangyur, one row records: this exact passage (named by its
stable citation and a fingerprint of its exact wording) corresponds
to this exact ACTib line (volume, page, line). Because the
fingerprint travels with the row, anyone can verify a match rather
than trust it — and we did: 99.5% of passages match ACTib's text
letter for letter, and the roughly 2,200 lines that differ are
listed side by side in `divergences.csv`, which doubles as a
ready-made proofreading worksheet for both projects.

ACTib's own content is not copied here — it stays at its home on
Zenodo (see "The join contract" below). This table is only the
layer of bookmarks and seals that lets the two resources be used
together, safely, however either one changes.

nabu-data's first re-publication: ACTib's known weakness is that its seg/POS layers carry no stable anchors into their source etexts (an upstream update orphans the whole layer — the concept doc's prior-art verdict), so this dataset publishes the anchor table that fixes it — one row per derge-kangyur passage tying URN + Passage_SHA256 to ACTib's (volume, page, line), with the measured match census as the in-band eval and the near/partial divergences republished as a proofreading table. The mapping is deterministic and measured (gold-derived); ACTib's own annotation layers stay labeled automatic upstream, and their 800 MB content is never republished — consumers join the DOI-cited Zenodo artifact on the anchor key.

## Maintenance

re-derive after a derge-kangyur or actib re-sync (the stale-ingest guard enforces freshness); every build re-measures the anchoring census into nabu.eval

## Provenance

Canonical inputs at derivation:

- `actib` @ `aef84458e2ecb0cd06e9e9f956533c3a79682926e0b8b457b7f1e7f16aab5b6e`
- `derge-kangyur` @ `a582cf471b7c85a101035071078032f106a8e536`

Recipe: xct/actib-anchors v1: anchor every live derge-kangyur passage (page.line citation grain) to its ACTib v2.0 SegPOS-eKangyur seg line (Zenodo 3951503): Esukhia volume N reads BDRC volume I1KG(9126+N) after the tail permutation {100→101, 101→102, 102→100}; folio→physical-page by walking each canonical volume's citation brackets in order (every new folio side increments the page counter, duplicated x-folio sides included, so [33xa]/[33xb] shift later folios; {D/T} Tohoku markers keep per-document folio maps so a mid-volume folio restart — the vol-31 Toh 11 seam, the census's vol-31 correction — resolves per document); line from ACTib's inline p<N>/ln<N> tokens (<utt> dropped); compare whitespace-free NFC letter streams — equal = exact, containment = partial, otherwise near with the exact Levenshtein distance in the Distance column; an absent ACTib line is missing, an unparseable ref is censused as badref, never guessed. The seg+POS token content is NOT republished: rows carry only the (ACTib_Volume, ACTib_Page, ACTib_Line) join key into the DOI-cited artifact plus the URN + Passage_SHA256 anchor into Nabu; near/partial rows republish both folded text forms in divergences.csv as the proofreading census. v1.1 layout (D55-b): anchors sharded per volume as anchors/<ACTib_Volume>.csv, each shard a self-contained CSV with its own header.

Derivation fingerprint: `c95c31be483806d6bfbcb0e56945f870225a70e8ad2f31e2f82cef1ae92dd7eb`.

## What a row means — the two-way anchoring contract

Each anchor row (`anchors/<ACTib_Volume>.csv` — one shard per volume,
every shard self-contained with its own header) ties one Derge
Kangyur passage to one ACTib line.
On the Nabu side, `URN` + `Passage_SHA256` name the exact catalog
passage bytes (rows apply only where the sha matches). On the ACTib
side, `(ACTib_Volume, ACTib_Page, ACTib_Line)` is the join key:
`ACTib_Volume` is the BDRC volume id as it appears in the artifact's
filenames (`UT4CZ5369-<ACTib_Volume>-0000.txt`), `ACTib_Page`/
`ACTib_Line` are ACTib's own inline `p<N>`/`ln<N>` markers. An empty
`ACTib_Line` means the page carries no line markers there (every
volume's title page, for one).

## The join contract — the layer content is NOT republished

This dataset deliberately contains none of ACTib's ~800 MB segmented/
POS-tagged text. Consumers take the DOI-cited artifact —
`SegPOS-eKangyur_July2020.zip` on Zenodo record 3951503
(doi:10.5281/zenodo.3951503) — and join its `seg/` or `pos/` volume
files on `(ACTib_Volume, ACTib_Page, ACTib_Line)`. License basis,
stated honestly: the Zenodo record declares CC BY 4.0; the zip itself
carries no license file — the record, not in-zip text, is the grant.

## The census — the measured anchoring quality

Of 461304 passages: 461199 compared —
458954 exact (99.51% of compared),
836 near (letter edit distance in `Distance`; histogram
{"1" => 603, "2" => 165, "3" => 52, "4" => 11, "5" => 1, "6" => 2, "8" => 1, "32" => 1}), 1409 partial
(one letter stream contains the other) — plus 102 missing
(no ACTib content at the mapped line) and 3 badref
(refs outside the citation grammar: `urn:nabu:derge-kangyur:toh3:7.39b.6:b2`, `urn:nabu:derge-kangyur:toh567:188a.7:b2`, `urn:nabu:derge-kangyur:toh7a:13.309b.1:b2`). Missing and badref
rows are censused here and in `nabu.eval`, never faked as anchor rows.
Comparison is on whitespace-free NFC letter streams; the same numbers
ride `datapackage.json` under `nabu.eval`.

## divergences.csv — the proofreading census

The near + partial rows again, WITH both folded text forms in-band
(`Nabu_Text` = the Derge passage's letters, `ACTib_Text` = ACTib's) —
the per-line divergence list a proofreader can act on directly.

## Loading

    import glob
    import pandas as pd
    anchors = pd.concat(
        (pd.read_csv(p, keep_default_na=False) for p in sorted(glob.glob("anchors/*.csv"))),
        ignore_index=True)

Note for tool authors: the datapackage declares ONE `anchors`
resource whose `path` is the ordered shard list; every shard
repeats the header (self-contained files beat strict multipart
concatenation for direct pandas/glob use — a deliberate, stated
deviation).

How to cite: reference ACTib (Meelen, Hill & Faggionato — the `actib`
key in `sources.bib`, DOI 10.5281/zenodo.3951503) alongside this
dataset's `datapackage.json` provenance block.
