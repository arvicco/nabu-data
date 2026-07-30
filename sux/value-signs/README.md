# Cuneiform value→sign table from the Oracc Sign List (readings, codepoints, concordances)

`sux/value-signs` — gold tier, anchoring: none. Produced by `nabu data build sux/value-signs` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

Flattens the Oracc Sign List (ex-OGSL, Veldhuis & Tinney, CC0 — the field's hand-curated sign registry) to one row per (value, sign) pair — OSL-spelled readings with stable @oid interop keys, Unicode codepoints (absence kept honest), value-level deprecation flags and in-band ambiguity, plus signs.csv/concordances.csv sidecars (variant forms, MZL/LAK/ABZL print-list numbers) — the table that upgrades Edubba's frequency instrument from value-counts to true sign-counts. The slug leads sux (Sumerian); the ~55 %akk-qualified readings ride the Language_Qualifier column — the scope call is stated in the dataset README.

## Maintenance

re-derive after each `nabu sync osl` (rolling master, no tags — a re-sync is an owner call; the stale-ingest guard enforces freshness); mechanical, no review needed beyond spot-checks

## Provenance

Canonical inputs at derivation:

- `osl` @ `7749a4bd8589491b987ab3da31660ef4abca5012`

Recipe: value-signs v1: canonical/osl/00lib/osl.asl (AslParser, NFC) flattened depth-first to one row per (value, sign-or-form record) — deprecated values INCLUDED and flagged (real corpora are transliterated with them), %lang qualifiers split into Language_Qualifier (empty = the sux scope the slug declares), Ambiguous = the Value spelling resolves to more than one record; sidecars signs.csv (one row per @sign/@form record, Parent_OID ties variants to their sign, @upua kept in PUA and out of Codepoints) and concordances.csv (one row per print-list token, List = the leading capital run); IDs v-<sha256(value|qualifier|oid|name)[0,12]> / s-<oid> / c-<oid>-<token>, positional -<n> on verbatim repeats.

Derivation fingerprint: `fff308682e97de2a45b97b85dc6b3e76163c7a517a50634264544a0988d4386c`.

## Language scope — sux leads, the %akk minority rides a column

OSL serves readings for Sumerian AND Akkadian (plus a handful of other
%-qualified languages). The slug's language call is **sux** (Sumerian):
the overwhelming majority of values are unqualified Sumerian readings,
and the downstream use (sign frequency over Sumerian corpora) is
Sumerian-first. The qualified minority — ~55 `%akk` values at the
2026-07-29 census, out of 11,238 `@v` lines — is kept, with the bare
qualifier token (`akk`, `akk/n`, …) in `Language_Qualifier`; an empty
cell means the default Sumerian scope. This is a stated scope
judgment, not a claim that every unqualified reading is exclusively
Sumerian.

## The grain — one row per (value, sign) pair

A value (reading) that resolves to several signs appears once PER
SIGN, each row flagged `Ambiguous` = `true` — ambiguity is visible as
multiple rows sharing a `Value`, never one candidate silently. A value
carried by a variant `@form` cites the form's own record (its `@oid`,
its encoding), and the form's parent sign is recoverable through
`signs.csv`'s `Parent_OID`. The primary key is the minted `ID` (values
carry subscript digits and `ₓ`, which cannot survive the CLDF
identifier class, so IDs are content digests); `OID` is the stable
Oracc identifier — the interop key for joining any Oracc-side
resource.

## Deprecation — included, flagged

Deprecated values (`@v-`) are INCLUDED with `Deprecated` = `true`:
real corpora were transliterated with them, so a frequency instrument
that dropped them would silently undercount. Filter them out with one
`Deprecated == "false"` clause if you want the current recommended
readings only. Deprecated SIGNS (`@sign-`) are flagged in
`signs.csv`; their values are not value-level deprecated unless
themselves marked.

## Codepoints — absence is honest

`Codepoints` is the space-separated Unicode scalar sequence
(`U+122C0 U+1200A`). An EMPTY cell means the sign is honestly
unencoded (~660 signs upstream have no encoding at all — that absence
is data). A partially encodable compound keeps upstream's bare `X`/`O`
placeholders verbatim inside the sequence. Private-use codepoints
(`@upua`) appear only in `signs.csv`'s `PUA` column, never in
`Codepoints`. `Glyph` is OSL's own rendered `@ucun` string where
present. Booleans are the strings `true`/`false`.

## The sidecars

`signs.csv` is the sign census: one row per `@sign`/`@form` record
(forms tied to their sign by `Parent_OID`), with `Aka` aliases
(`;`-separated), sign-level deprecation, `Unicode_Name`, and the
encoding columns above. `concordances.csv` flattens the print-list
numbers (`@list`): one row per (record, token), `List` = the list
code (MZL, LAK, ABZL, …), `Number` = the rest verbatim (`127`,
`039^b`).

## Loading

    import pandas as pd
    df = pd.read_csv("value-signs.csv", keep_default_na=False)
