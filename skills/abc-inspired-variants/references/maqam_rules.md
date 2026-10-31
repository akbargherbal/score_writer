# Maqam rules (12-tone approximations) for Ajam, Hijaz, Kurd, Nahawand

The agent must make every variant obey the target maqam. `scripts/abc_tool.py modal` enforces the
numeric part; this file supplies the musical part. Degrees are counted from the tonic (1 = home note,
the "qarar"); `b` means a semitone lower than the major-scale degree.

**Honesty about this file.** It is a compact summary of mainstream Arabic maqam theory, flattened to
12 tones because the ABC scores and abcjs playback are 12-tone. Real Hijaz, Kurd etc. use slightly
different microtonal inflections, and regional practice varies. The user's ears and corrections
override this file. When he corrects something, record it in `FEEDBACK_LOG.md`.

## Contents
1. At a glance
2. Ajam
3. Hijaz
4. Kurd
5. Nahawand
6. Shared principles (home note, sayr, cadence)
7. Twin-mode trap
8. Compliance checklist for each variant

## 1. At a glance

| Maqam | Scale (semitones from tonic) | Degrees | Western cousin | Must be heard | Must NOT appear (beyond passing notes) |
|---|---|---|---|---|---|
| Ajam | 0 2 4 5 7 9 11 | 1 2 3 4 5 6 7 | major | 3 and the leading tone 7 | b3, b6 |
| Hijaz | 0 1 4 5 7 8 10 | 1 b2 3 4 5 b6 b7 | Phrygian-dominant | b2 and 3 together (the augmented second) | b3, 2 |
| Kurd | 0 1 3 5 7 8 10 | 1 b2 b3 4 5 b6 b7 | Phrygian | b2 and b3 | 2, 3, 6 |
| Nahawand | 0 2 3 5 7 8 10 | 1 2 b3 4 5 b6 b7 | natural/harmonic minor | 2 and b3 | b2, 3 |

Tolerated "colour" guests (limited to about 12% of a voice's time, the tool counts them at half weight):
Ajam b7; Hijaz 6 and 7; Nahawand 7 (the raised seventh, harmonic-minor colour). Kurd has none.
Anything else counts as outside the maqam; the tool allows only a few percent for passing notes.

**The scale degrees inside the maqam are not "cleanliness": they are the song's colours.** A Nahawand line that
spends 12% of its time on b7 is not sloppy, it is the mode. When you edit a source, match its own degree mix
(`features` prints `degrees_pct`); do not bleach the colour degrees to zero.

## 2. Ajam
- Structure: Ajam jins (1 2 3 4) on the tonic, joined at the 5th with another Ajam jins (5 6 7 8).
- Feel: bright, major. The 3 must be major and the 7 should appear (at least in cadences as a leading tone).
- Home 1, dominant 5. The 3 and the 5 are strong resting points; the 6 is a common launching note for the
  upper part.
- Cadence: 7 -> 1 (leading tone) or 2 -> 1 descending, or 5 -> 1.
- Common error: slipping in b3 or b6 makes it sound Nahawand. The tool flags it.
- Optional, low-confidence colour: a lowered 7 (b7) briefly in the upper area.

## 3. Hijaz
- Structure: Hijaz jins on the tonic (1 b2 3 4: semitone, augmented second, semitone), then an upper
  jins on the 5th. Upper jins commonly Nahawand-like (5 6 b7 8 or 5 b6 b7 8) or Hijaz again on the 5th.
- Identity: the **augmented second between b2 and 3**. If the line never moves b2 <-> 3, it is not Hijaz.
  The semitone b2 -> 1 is the other signature: descend onto the tonic from b2.
- Home 1, dominant 5 (the 4 is also a frequent stopping note). The 3 is a stable colour note; do not
  confuse it with b3, which belongs to Kurd/Nahawand.
- Cadence: b2 -> 1, or 3 -> b2 -> 1 (the descending signature), or 5 -> 4 -> 3 -> b2 -> 1.
- Common error: using b3 (sounds Kurd) or the plain 2 (sounds like a different maqam).
- 12-tone note: real Hijaz uses microtonal inflection; here it is the plain 0 1 4 5 7 set.

## 4. Kurd
- Structure: Kurd jins (1 b2 b3 4: semitone, tone, tone) on the tonic; upper part 5 b6 b7 8.
- Identity: the **b2 sitting directly above the tonic** together with b3. It is Nahawand without the
  natural 2 and with a "dark" step at the bottom.
- Home 1, dominant 5. The b3 is a strong resting point.
- Cadence: b2 -> 1 (semitone) and b3 -> b2 -> 1; also 4 -> b3 -> b2 -> 1.
- Common error: a natural 2 (turns it into Nahawand) or a major 3 (turns it into Hijaz).

## 5. Nahawand
- Structure: Nahawand jins on the tonic (1 2 b3 4: tone, semitone, tone), upper jins on the 5th, either
  Kurd-like (5 b6 b7 8, the natural-minor form) or Hijaz-like (5 b6 7 8, the harmonic-minor form, the
  raised 7 with the augmented second b6 -> 7).
- Identity: natural 2 plus b3, no b2. The pair 2 <-> b3 and the b3 as a resting place.
- Home 1, dominant 5. Ascending lines may use the raised 7 (colour), descending lines usually use b7.
- Cadence: 2 -> 1, b7 -> 1 (descending), or 7 -> 1 (harmonic colour).
- Common error: a b2 (turns it Kurd) or a major 3 (turns it Ajam).

## 6. Shared principles

- **Home note.** A maqam needs an audible home. The last Vocal note of the piece is the tonic. A real share of
  phrases should come to rest on it (or on the 5th, which is also a resting note) — but the *rate* is the source's
  own: if the source ends two of eight lines on the 3rd or the 2nd, keep that. Do not turn every line into the same
  cadence; that is what made the first batch of variants sound like an exercise.
- **Sayr (melodic journey), common practice, not a law.** Open around the tonic or the 3rd, establish the dominant,
  rise into the upper jins for the climax, come back down to the tonic. Use it to *decide what to change*, not as a
  licence to rewrite: in an edit, the sayr is already there. Only the part you recompose follows this from scratch.
- **Cadence formulas** above are where a maqam is recognised. Use them at the section ends you actually rewrite.
- **Skips.** Large leaps are fine when they land on 1, 3(b3), 5 or 8; unprepared leaps onto the characteristic
  degrees (b2, 3 in Hijaz) sound arbitrary.
- **Transposition is free, structure is not.** Write the maqam on any tonic; the spelling is tonic-relative and
  `scale` prints the exact ABC letters for the file's `K:`.

## 7. Twin-mode trap (why detection can be uncertain)

In 12 tones some maqams share exactly the same notes: Ajam on C = Nahawand on A (natural minor) =
Kurd on D. Only the home note and the endings separate them. When the tool lists CLOSE RIVALS, decide by
where phrases come to rest and where the song ends, and when still unsure, follow the folder label
(the user's AI labeller was about 80-90% right).

## 8. Compliance checklist for each variant

A variant is a repair of a score that already passed these tests. So:

1. `abc_tool.py modal VAR.abc --maqam M --tonic T` prints OK with no FIX lines.
2. The characteristic move still appears where the source had it (first two sung phrases, and in the chorus).
3. **The source's cadence behaviour is preserved**: phrases that rested on 1 or 5 still do; a section the source
   deliberately left open (ending on 2 or b3) may stay open. Only the final note of the piece must be the tonic —
   and if the source ends elsewhere, that is a named weakness to repair, not a rule to impose on every phrase.
4. The `Ins` voice obeys the same scale (the tool allows it slightly more freedom for passing notes).
5. The degree mix (`features`, `degrees_pct`) is close to the source's. Losing a colour degree the source leans on
   (b7 in Nahawand, 6 in Hijaz) is a `character` FIX from `verify`, not a "cleaner" result.
