# Tibetan script ↔ EWTS (Wylie) neutralization rule table

`xct/wylie-fold` — gold tier, anchoring: none. Produced by `nabu data build xct/wylie-fold` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

A hand-curated transliteration rule table letting Tibetan-script and Wylie-romanized text meet in one query space — doubles as the source for Nabu's generated Tibetan transcoder module.

## Maintenance

on rule corrections only; each change re-derives the Tibetan shelves (fold modules are fingerprinted derivation inputs)

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: authored Tibetan↔EWTS rule table (config/ewts/rules.csv, sha256 3efca8b22e8c2df0e6e2dd5fcbe3e7e6387f18ae406e2b072541de7778d9731e); the generated Nabu::Xct transcoder derives from the same table via rake fold:xct

Derivation fingerprint: `7072dbb17688d0b755d6b44c90d7dd4c55b7aa0838234f05c855cd92c56735a0`.

## Scope and honest limits

The table is the WORKING CORE for real canon text, not the whole
Tibetan block: the 30 native consonants, the retroflex Sanskrit-loan
letters (T/Th/D/N/Sh), the subjoined series (which, in NFC, also
carries the decomposed aspirates: gha = U+0F42 U+0FB7), the vowel
signs including a-chung A and the Old Tibetan reversed gi-gu (-i),
anusvara/visarga/candrabindu, the head marks, tsheg/shad, and the
digits. Deliberately NOT curated (pass-through in the transcoder):
subjoined a-chung/a-chen (U+0FB0/U+0FB8), the fixed-form ra/wa/ya
(U+0F6A, U+0FBA–0FBC), halanta (U+0F84), tsa-'phru (U+0F39), the
rare marks U+0F82/U+0F86/U+0F87, and ornamental punctuation
(U+0F06–0F0A, U+0F0F–0F1F) — honest smaller table over speculative
completeness.

The generated transcoder concatenates stack letters WITHOUT the EWTS
"+" operator (query-form grain: bsgrubs, not b+s+g+r+u+b+s) and
resolves the vowel-less three-letter syllables the classical grammar
leaves genuinely ambiguous by preferring the prefix reading, with a
curated override list for the attested common words (མངས = mangs,
never mngas; བགས = bags). The precomposed NFC-excluded codepoints
(U+0F43 etc.) never occur in NFC text and are intentionally absent.

## Language scope (the bod call)

languages.csv lists xct (Classical Tibetan) — the slug's language and
the holdings this fold serves first (Derge Kangyur/Tengyur, SOAS
gold). The rules themselves are SCRIPT-level and apply unchanged to
Old Tibetan (otb) and modern bod: inside Nabu the transcoder
registers for xct, bod AND otb query folding. The dataset keeps the
one-language-per-feature rail contract and states the wider
applicability here instead of duplicating rows.
