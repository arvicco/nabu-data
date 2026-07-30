# Kanripo gaiji display ladder — faithful/IDS/substitute resolutions for &KR…; references

`lzh/kanripo-gaiji` — gold tier, anchoring: none. Produced by `nabu data build lzh/kanripo-gaiji` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

The hand-curated resolution ladder for the Kanseki Repository's not-yet-encoded character references (427 faithful codepoints, 562 labeled substitutes, the IDS lane empty by census, everything else an honest ⬚ placeholder) — the same three TSVs Nabu's `--display reading` mode loads for lzh kanripo passages. BY-SA: curated from KR-Gaiji's charlist under the kanripo org grant (CC BY-SA 4.0).

## Maintenance

re-curate by hand after a `nabu sync kr-gaiji` advances charlist.org.txt (the P38-1 procedure); the curation is pinned to the charlist commit its file headers record, deliberately never auto-derived

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: lzh/kanripo-gaiji v1: the hand-curated Kanripo gaiji display ladder (kanripo.tsv sha256 89956448a6d59bbe3af7305fc9862a0478508681991d3cfb8a2364b6282f4a1f; kanripo-ids.tsv sha256 9c9d0b5c33f25556447c0d8962a55b4f46eb817ed63e9ab60636daa593587f2a; kanripo-substitutes.tsv sha256 d0092358314319e1492f28ba7a1d2dc2dd9b15ff0a6f9d7391ab46b286ba8936), curated from KR-Gaiji charlist.org.txt @ 662fd61d (github.com/kanripo/KR-Gaiji) — the same three TSVs Nabu's `--display reading` mode loads for kanripo passages

Derivation fingerprint: `3d53956f04a9824664208b4095888ed0f175729380de8d26d39b2bd44527484e`.

## The ladder — four rungs, three lanes

Kanripo text repos embed `&KR\d+;` references for characters not
yet encoded in Unicode. The display ladder resolves each reference
per character, in four descending rungs: **faithful** (a real
assigned codepoint that IS the character), **IDS** (an Ideographic
Description Sequence — shown when no single codepoint fits),
**substitute** (a lossy standard-character normalization, a
scholar's read-through — labeled as such, never merged with
faithful), and finally the honest **⬚ placeholder** (U+2B1A) for
the 4265 refs of the charlist's 5,254 that none of
the lanes resolves — a rung-4 ref is the ABSENCE of a row here,
never a fake glyph. An upper rung always wins: the lanes are
disjoint by ref (validated at build time).

The IDS lane ships EMPTY by census, not by omission: the charlist
holds exactly one column-3 composition (KR0198 `[沔-丏+丐]`), and
its resolution ⿰氵丐 is an encoded glyph form of 沔 (U+6C94), so it
lands in the faithful lane. The lane's shape is published so IDS
resolutions have a home when curation adds them.

## Provenance of the curation

Hand-curated (the P38-1 honesty gates: single real assigned
codepoint, no Private-Use-Area rows, NFC, uncertain `?`-marks and
multi-character cells dropped) from KR-Gaiji `charlist.org.txt` @
662fd61d (2019-11-30), reconciled against Unihan and
BabelStone IDS. Curation-time coverage census: faithful rows cover
36.55% of all 1,751,360 gaiji occurrences in the kanripo corpus,
substitutes a further 45.25% (cumulative 81.80%). The curation is
pinned to that charlist commit — deliberately NOT re-derived at
build time — so this dataset declares no canonical inputs; its
derivation identity is the recipe's three file sha256s. When
upstream advances: `nabu sync kr-gaiji`, re-curate, rebuild.

These resolutions serve Literary Chinese (lzh) kanripo passages;
inside Nabu the same three files feed `--display reading`.
