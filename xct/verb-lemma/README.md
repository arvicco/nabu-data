# Tibetan verb stem → paradigm-lemma map (from the Tibetan Verb Database)

`xct/verb-lemma` — gold-derived tier, anchoring: none. Produced by `nabu data build xct/verb-lemma` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

Maps the 2,491 TVD stem tuples (present/past/future/imperative, grammarians' disagreements kept uncollapsed) to a paradigm lemma, enabling verb-form-aware lookup across Classical Tibetan. The table half only: the anchored layer over the canon is deferred behind xct/segmentation.

## Maintenance

re-derive after tibetan-verbs sync; upstream is stable (CC0)

## Provenance

Canonical inputs at derivation:

- `tibetan-verbs` @ `ca6ba75066aa8cfd53631d0f3ad0350e026b8b4e`

Recipe: verb-lemma v1: canonical/tibetan-verbs/db.csv expanded to one row per (stem tuple × attesting source tag TDC/PH/GT/KN, read from the cell value, not the column position) — disagreements uncollapsed, empty stems stay empty, values NFC-normalized, Tibetan script only (no transliteration); Lemma = the present stem; ID = v-<sha256(stem tuple)[0,12]>-<source>, positional -<n> when upstream restates a (stems, source) row. Table half only: the anchored layer over the canon is deferred behind xct/segmentation.

Derivation fingerprint: `aa7a32e1c64fd8f8d4d73a610e6d302ea9415cf32379e8d5f5823a24a146f1ca`.

## Scope — the table half only

This release is the verb-stem table alone. The anchored layer over the
canon (stem occurrences pinned to passage URNs in the Tibetan corpora)
is explicitly deferred: it depends on tsheg-bar/word segmentation,
which lands with `xct/segmentation`. Anchoring here is `none` by
design, not omission.

## The grain — one row per grammarian-analysis

The TVD deliberately preserves its sources' disagreements ("no choice
has been made about the correctness of the different forms" — upstream
README). This table keeps them uncollapsed and goes one step finer:
each upstream stem-tuple row becomes one row per attesting source, so
`Analysis_Source` always names exactly one authority — the values
(`TDC`, `PH`, `GT`, `KN`) are the TVD's own source tags, verbatim; see
the upstream repository's bibliography for the works behind them.
Filtering on one `Analysis_Source` value yields that authority's
complete verb table. Note that `(Lemma, Analysis_Source)` is NOT
unique — one authority can give several paradigms for one present
stem — and upstream even restates one `(stems, source)` row verbatim,
so the primary key is the minted `ID`.

## Columns

`Lemma` is the paradigm lemma — the present stem (ད་ལྟ), the citation
form. `Present`/`Past`/`Future`/`Imperative` carry the stems in
Tibetan script as upstream gives them (NFC-normalized; upstream's
second-suffix-ད / alternate-orthography notation `༼ད༽` kept verbatim).
An empty cell means the authority gives no such form — absence is
honest, never filled in. Upstream carries no Wylie romanization, so
none is published here: transliteration belongs to `xct/wylie-fold`.
`Language_ID` is `xct` (Classical Tibetan) throughout — upstream
carries no language tagging of its own; the one-tag call is stated in
the producer contract.

## Loading

    import pandas as pd
    df = pd.read_csv("verb-lemma.csv", keep_default_na=False)
