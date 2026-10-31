# Maqam recipes — starting points for A / B / C

**A starting point, not a ceiling.** Take what helps, combine it, bend it, or ignore all of it. If you know a better
move for *this* song, use it: you know more music than this page does. The page exists to save you thinking time on
the common cases and to give you spellings that are already checked.
If the task text contains `NO_RECIPES`, skip this file entirely (that is the control condition of an experiment).

## Contents
1. What this is, and how sure it is
2. Using it
3. Where it tends to fit
4. Hijaz  5. Nahawand  6. Ajam  7. Kurd
8. The report line

## 1. What this is, and how sure it is

- **Provenance: general knowledge of the Western cousin mode plus mainstream maqam theory. Not yet checked against the
  user's songs.** Treat every item as a hypothesis, and say so in the report when you lean on one.
- **What is verified:** each ABC example below passed `check`, `lint` and `modal` for its maqam (tonic D): the notes are
  legal. That says nothing about whether they sound good, and you cannot hear; say that too.
  (Nahawand and Ajam sketches get a `WARN` that the characteristic move appears only once or twice: expected in four
  bars, and it disappears in a full section.)
- **About chords.** The source's chord track comes from an automatic chord recogniser, and it is often plain
  minor/major (`C#m`, `G#`) sitting under a Hijaz melody. That friction is part of the sound he heard and liked, so the
  "chords" lines below are *palettes of options*, never a verdict that a chord is wrong. Keeping the source's own chords
  is still the default (SKILL.md rule 9); reach for a palette only when a bar's melody changed enough that you want a
  different chord there.
- Recipes speak in scale degrees. Turn them into letters with `scale` for the song's tonic and `K:`.

## 2. Using it

- Use as many or as few items as serve the song. Mixing two recipes' ideas, or inventing something that is not here,
  is welcome. Say what you did in one line.
- **Fit the song's own rhythm.** An example written in a different pulse sounds foreign in this singer's delivery;
  `features` gives the median note length, repeated-note share and leap share to match. This is craft, not a rule.
- **Vary between songs.** If the same figure appears in every song of a batch, the batch loses its character. Change the
  rhythm, an interval or the starting degree.
- **The song is evidence.** If its habits differ from a recipe (it ends lines on 3 rather than b2, say), that is what he
  likes: follow the song.
- If `verify` raises a fidelity or character `FIX` after you used something from here, read it as "this pulled the song
  too far from its source" and soften that item. The recipe is not wrong; it just did not fit this song.

## 3. Where it tends to fit

| Part | A Enhance | B Recompose | C New hook |
|---|---|---|---|
| Cadence formulas | the repaired cadence | cadences of the rewritten section | end of the new chorus |
| `Ins` riff shapes | the one new figure that returns | a line answering the section | the counter-line |
| Contour / lift ideas | usually not needed (A keeps the melody) | the section you rewrite | the new chorus |
| Chord palette | only if you changed a bar's chord | same | same |

This table is a suggestion about where the ideas pay off, not a list of permissions.

## 4. Hijaz  (Phrygian dominant; tonic D: D Eb F# G A Bb C)

- **What makes it Hijaz:** the augmented second b2 <-> 3 (Eb <-> F#) and the semitone fall b2 -> 1.
- **A typical journey:** begin on 1 / 3 / 5, linger on 5, climb into the upper cell (5 b6 b7 8), come home 4-3-b2-1.
- **Cadences (degrees):** `3 b2 1` (hold the b2) · `5 4 3 b2 1` · `b2 1`.
- **Contour ideas:** recite on 1 then step into the augmented second (`1 1 1 1 b2 3 3 b2 1`) · leap 1 -> 5 then walk
  down `4 3 b2 1` · for a lift, start the same contour a fourth higher so the apex reaches 8 or the b2 above it.
- **`Ins` riff shapes (5-7 notes):** `1 b2 3 b2 1 b7 1` · `5 4 3 b2 3 b2 1`.
- **Chord palette:** sits comfortably `D`, `Eb`, `Gm`, `Cm`, `Bb`. Creates friction with the melody (can be deliberate
  colour; the source often does it): `Dm`, `Am`, `A`, `C`, `Em`. Typical loops: `D Eb D` · `D Eb Cm D` · `D Gm D Eb`.
- **What tends to change the maqam's identity (good to know, fine to use as colour):** b3 or the natural 2 pulls it
  toward Kurd/Nahawand; phrases that end on 3 without passing b2 start to sound major.
- **Verified ABC (D, K:Dm):**
```
"D"D2D2D2D2|"D"_E2^F2^F2_E2|"Gm"A4G2^F2|"Eb"_E4"D"D4|      (hook sketch, 4 bars)
D2_E2^F2_E2|D2C2D4|                                         (Ins riff, 2 bars)
```

## 5. Nahawand  (natural/harmonic minor; tonic D: D E F G A Bb C, colour C#)

- **What makes it Nahawand:** natural 2 with b3 (E <-> F); b3 is a resting place. The raised 7 (C#) is colour on the way
  up; b7 on the way down.
- **A typical journey:** begin around 1-b3, establish 5, climb through `b6 b7 8`, descend to 1.
- **Cadences:** `2 1` · `b7 1` · `7 1` (harmonic-minor colour).
- **Contour ideas:** `1 2 b3 b3 2 1` (compact, singable) · rise `5 b6 b7 8` then fall `b7 b6 5` · for a lift, move the
  apex to 8 or 9 and rest on a high b3.
- **`Ins` riff shapes:** `1 2 b3 2 1 b7 1` · `5 b6 5 4 b3 2 1`.
- **Chord palette:** sits comfortably `Dm`, `Gm`, `Am` (natural v) or `A` (harmonic v), `Bb`, `C`, `F`. Friction: `Eb`, `D`
  (a major ending is a classic exception), `E`, `F#`. Typical loops: `Dm Bb C Dm` · `Dm Gm C F` · `Dm C Bb A`.
- **What tends to change its identity:** b2 turns it toward Kurd; a major 3 toward Ajam.
- **Verified ABC (D, K:Dm):**
```
"Dm"D4E2F2|"Gm"F2G2A4|"Bb"B4A2G2|"Am"E4"Dm"D4|
D2E2F2E2|D2C2D4|
```

## 6. Ajam  (major; tonic D: D E F# G A B C#)

- **What makes it Ajam:** the major 3 and the leading tone 7; bright. Resting places: 3 and 5.
- **A typical journey:** open on 3 or 5, rise to the upper 1, descend by steps to 1.
- **Cadences:** `7 1` · `2 1` · `5 1`.
- **Contour ideas:** `3 3 3 5 | 4 3 2 1` · leap 5 -> 8 then descend · for a lift, put the apex on the upper 1 (or 2).
- **`Ins` riff shapes:** `5 6 7 8 7 6 5` · `3 2 1 2 3 5 3`.
- **Chord palette:** sits comfortably `D`, `Em`, `F#m`, `G`, `A`, `Bm`. A touch of `C` gives the b7 colour. Friction: `Dm`, `Bb`,
  `F`, `Gm`. Typical loops: `D A Bm G` · `D G A D` · `Bm G D A`.
- **What tends to change its identity:** b3 or b6 slides it to Nahawand; long rests on 6 do too (Ajam on D has the same
  notes as Nahawand on B, so the ending decides which one it is).
- **Verified ABC (D, K:D):**
```
"D"F2F2F2A2|"G"G2F2"A"E2"D"D2|"Bm"B4A2F2|"A"E2c2"D"d4|
A2B2c2d2|c2B2A4|
```

## 7. Kurd  (Phrygian; tonic D: D Eb F G A Bb C)

- **What makes it Kurd:** b2 directly above the tonic together with b3; dark. The semitone fall b2 -> 1.
- **A typical journey:** stay low around `1 b2 b3`, climb to 5 and `b6 b7`, return through `4 b3 b2 1`.
- **Cadences:** `b2 1` · `b3 b2 1` · `4 b3 b2 1`.
- **Contour ideas:** `1 1 b2 1 | b3 b3 b2 1` · `5 4 b3 b2 1` · for a lift, the same cell a fourth up.
- **`Ins` riff shapes:** `1 b2 b3 b2 1 b7 1` · `5 b6 5 4 b3 b2 1`.
- **Chord palette:** sits comfortably `Dm`, `Eb`, `F`, `Gm`, `Bb`, `Cm`. Friction: `Am`, `A`, `D`, `E`, `C`. Typical loops:
  `Dm Eb Dm` · `Dm Cm Bb Cm` · `Dm Eb F Gm`.
- **What tends to change its identity:** a natural 2 turns it toward Nahawand; a major 3 toward Hijaz.
- **Verified ABC (D, K:Dm):**
```
"Dm"D2D2_E2D2|"Eb"F2F2_E2"Dm"D2|"Gm"G4F2_E2|"Cm"_E4"Dm"D4|
D2_E2F2_E2|D2C2D4|
```

## 8. The report line

In `VAR_REPORT.md` section 6, add two short lines per variant:
- `Recipe use: <none | cadence "3 b2 1" | Ins riff shape 2 | contour 1 | ...>` (hypothesis, unverified on the corpus).
- `My own ideas beyond the recipe: <what you tried that is not on this page, or "none">`.

If you did not open this file (`NO_RECIPES`, or nothing new was written), write `Recipe use: none`. These lines are how
the experiment is read: whether the page helped, and whether you went further than it.
