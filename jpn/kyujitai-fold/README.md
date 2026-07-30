# Japanese kyūjitai↔shinjitai reform-pair census (Unihan jinmeiyō + KANJIDIC2 jōyō lanes)

`jpn/kyujitai-fold` — gold tier, anchoring: none. Produced by `nabu data build jpn/kyujitai-fold` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

The two-lane old↔new kanji pair table (Unihan kJinmeiyoKanji reform pairs + KANJIDIC2 jōyō-target variant edges, reform merges admitted, refusals censused) rendered through the same resolution seam `rake fold:jpn` compiles into Nabu::Jpn — one seam, two consumers. BY-SA: the load-bearing KANJIDIC2 lane is EDRDG share-alike (CC BY-SA 4.0).

## Maintenance

re-derive after each unihan/edrdg sync (EDRDG rebuilds nightly, Unihan annually); regenerate together with `rake fold:jpn` so the shipped fold module and the dataset never drift

## Provenance

Canonical inputs at derivation:

- `edrdg` @ `9ef970a92e19d35c481808f6dae3663c70c984ebc9f05b1834354c5fabb92ea9`
- `unihan` @ `8bf47834ffe25d222e298d4f8c890621546bd0b59e8be631c3dd28f2cb35eabf`

Recipe: jpn/kyujitai-fold v1: two-lane kyūjitai↔shinjitai pair census rendered through Nabu::Ops::JpnFoldBuilder — the same resolution seam `rake fold:jpn` compiles into Nabu::Jpn, Nabu's jpn search fold. Lane 1 (jinmeiyo): Unihan kJinmeiyoKanji 1:1 reform pairs, NFC-identity compat pointers dropped. Lane 2 (kanjidic): KANJIDIC2 jis208/jis213 variant edges (decoded through the held JIS X 0213 table; jis212 refused — a different standard) whose target is jōyō = KANJIDIC2 grade 1–6/8 ∩ Unihan kJoyoKanji (D38-b), reform merges admitted per the 2026-07-21 owner ruling; one-to-many ambiguous olds and jinmeiyō-lane conflicts refused into refusals.csv. A kanjidic edge duplicating a jinmeiyō pair is emitted once, under lane jinmeiyo.

Derivation fingerprint: `2d87174a7f206f8e9d979a57c79a9550d7248a65d1b84533539e57971303420a`.

## The two lanes — and what a row asserts

`Lane=jinmeiyo` rows are Unicode's own kJinmeiyoKanji reform pairs:
the SEMANTIC kyūjitai relation (the character card's old/new
cross-reference). `Lane=kanjidic` and `Lane=kanjidic-merge` rows are
FINDABILITY edges mined from KANJIDIC2 variant links under the
jōyō-target policy — not all of them are genuine "old forms" (弃 is
棄's ancient form), so they feed search folding, never the semantic
relation. A merge row's new form is shared by 2+ old claimants
(辨/瓣/辯→弁): distinct classical words the script reform collapsed,
admitted deliberately to match modern reading habits.

Inside Nabu the same census compiles (via `rake fold:jpn`) into the
jpn search fold, whose fold TARGET composes through the Han
traditional/simplified table so Japanese and Chinese forms land on
one skeleton — this dataset publishes the pair relation itself and
leaves skeleton composition to the consumer's Han table.

## The census (this derivation)

- jinmeiyō 1:1 pairs: 173
- kanjidic 1:1 singles: 341
- kanjidic merges: 79 new forms ← 185 old claimants
- refused (refusals.csv): 2 one-to-many ambiguous, 0 jinmeiyō-lane conflicts
- dropped silently by policy: 57 NFC-identity compat pointers (they cannot survive NFC text); all jis212 variant links (JIS X 0212 is a different standard than the JIS X 0213 table used for decoding)

Upstream at derivation: Unihan 17.0.0 (file date 2025-07-24),
KANJIDIC2 2026-210 (date of creation 2026-07-29).

## Licensing

The jinmeiyō lane derives from Unihan (Unicode License V3); the
kanjidic lanes derive from KANJIDIC2, which the EDRDG makes
available under CC BY-SA 4.0. The combined table is therefore
published CC BY-SA 4.0 (see sources.bib for the required
attributions), overriding the nabu-data repository default.
