---
name: abc-inspired-variants
description: Takes ABC-notation scores (auto-transcribed from AI-generated songs, e.g. REF_ABC_SCORE_MAQAM/<Maqam>_Shortlist/<song>/score.abc) and writes three EDITED versions of each score — VAR_A_score.abc (Enhance), VAR_B_score.abc (Recompose one part) and VAR_C_score.abc (New hook) — plus a short Arabic report. The source is the song and stays the song: melody, rhythm, meter, chords and accompaniment are preserved and only named weaknesses are repaired. For the "arabmaqamrock" project (Arabic maqam symphonic rock, Suno/YuE2 LoRA); the user has no music education and reads Arabic. Use whenever the user shares .abc files, a folder of scores, or pasted ABC text, mentions "score", "سكور", "abcjs", "YuE2", "native ABC", "chords", "كوردات", "نكهة", "استلهام", "variants", "VAR_A", "Shortlist", "مقام", "حجاز", "كرد", "نهاوند", "عجم", "قمر بغداد" or arabmaqamrock, or asks for melodies, hooks, fills or improved versions of a score, or gives feedback on earlier variants, even without saying "skill" or "ABC". Not for identifying which song a score comes from.
---

# ABC Inspired Variants (autonomous mode)

**A variant is an edit of the song, not a new song.** He generates tracks *from* these files; whatever the variant
loses, the track loses. The source track was rated 8/10; the tracks generated from the first batch of variants were
rated 6.5 ("not impressive at all"). The variants were not wrong notes — they were a **cleaner, flatter, quieter
rewrite** of a melody he already liked. Every rule below exists to stop that.

Read this once before composing:

| | the source | what a "flattened" variant did | what it cost |
|---|---|---|---|
| median sung note | 0.23 s | 0.46 s | the words stop sounding like this singer's delivery |
| repeated pitches (recitation) | 31% | 3% | the declamatory Arabic pulse disappears |
| stepwise moves | 53% | 88% | every leap, every jump of character, gone |
| notes in b7 | 12% | 2% | the mode's own colour is bleached |
| meter | 2/4 with 3/8 and 1/4 bars | 2/4 everywhere | the opening's 3/8 "step" is smoothed away |
| second voice | a real arrangement line (~15% of the time, 29-semitone span) | a few 3-note fills in one octave | the counter-line disappears |
| chords | 138 symbols (abcjs plays them) | none | the accompaniment he hears in abcjs is gone |

Pleasant, tidy, and not his song. Do not do this.

## Operating rules

1. **Never stop to ask a question.** Choose the most reasonable default, apply it, write the assumption in the
   report, finish the batch.
2. **Never modify `score.abc`.** Write `VAR_A/B/C_score.abc`. Do not overwrite existing variants unless he said
   "regenerate" (then use `_r2`, `_r3`). If all five outputs exist for a song, skip it. When he rejects a whole
   batch, move it to `rejected_r1/` (never delete: he may want to compare) and write the new one with `_r2`.
3. **You cannot hear.** Never say a variant "sounds better". Say what changed and what to listen for.
4. **Start from a copy of `score.abc` and edit it.** Never compose three files from a blank page: copying is what
   keeps the meter changes, the chords, the rhythm and the register alive. `cp score.abc VAR_A_score.abc`, then
   edit bars. Every note you did not touch is a note the generator still gets right.
5. **Keep the identity.** Melody, rhythm, meter scheme, chords, tempo, register and the second voice's role are
   preserved unless your recipe explicitly names them as the thing to change. The tool enforces this with FLOORS
   (see step 5); a variant under the floor is returned as `FIX`, however pretty it is.
6. **Repair, do not replace.** Each variant targets 1-2 named weaknesses of the source (step 1b) and must leave
   everything else alone. Removing the source's quirks is not an improvement.
7. **Maqam correctness is a hard requirement**, checked by the tool, not by your impression.
8. **Keep the source's dialect** (`references/native_dialect.md`): two voices, the source's `L:` and `K:`, its `M:`
   scheme, section comments, no tuplets/grace notes/slurs/repeats/`w:` lines. `lint` must be clean.
9. **Keep the chords** (rule changed): the source's chord symbols are part of the sound he hears in abcjs and part of
   what the generator receives. Carry them over with `chords-from` unless the melody of that bar changed so much
   that the chord no longer fits — then replace it with a chord from the same scale and say so in the report.
10. **Do not try to name the song.** The fingerprint tools are for deciding what to keep and what to repair.

Read `references/project_context.md` (what ABC can and cannot do, what is known) and
`references/native_dialect.md` once per run. If `FEEDBACK_LOG.md` exists in the data root, read it and follow it;
it outranks the defaults here.

## Input and output layout

```
<root>/                          e.g. REF_ABC_SCORE_MAQAM
  Hijaz_Shortlist/<song>/score.abc        <- input; the folder name gives the label
                    /VAR_A_score.abc      <- Enhance
                    /VAR_B_score.abc      <- Recompose one part
                    /VAR_C_score.abc      <- New hook
                    /CONTROL_score.abc    <- source melody, chord-free, notes verified identical
                    /VAR_REPORT.md
                    /rejected_r1/         <- a batch he rejected (kept, never deleted)
  VARIANTS_INDEX.md
  FEEDBACK_LOG.md
```

Labels (`Ajam_/Hijaz_/Kurd_/Nahawand_Shortlist`) come from an AI labeller, 80-90% right: a prior, not a fact.
Tool: `python scripts/abc_tool.py …` (`python3` if that is what exists; quote paths with spaces/backslashes).
`progress <root>` lists songs still lacking outputs. A single score with no folder, or pasted ABC: treat as one song,
write next to it (`abc-inspired-variants-out/` if pasted only).

## Per-song pipeline

### 1. Measure
```
python scripts/abc_tool.py brief <song>/score.abc --label <Label>
```
Then inspect the file itself (voices, `M:` lines, section comments, bar count). Transcribers re-guess tempo, meter
and key per file, so compare per-second and per-phrase numbers, not raw note units.

Write down three things:

**(a) Flavor card** — 2-3 traits where `traits` shows |z| >= 1 (or, if none, the song's most distinctive numbers).
Say in the report that it comes from numbers only. These traits are **what to protect**, not what to fix.

**(b) Weakness list** — 2-4 concrete weaknesses, each with a bar range and a reason. Look for:
- a section that is lower in energy than the one before it (mean pitch, apex, or apex position late in the section);
- the highest note of the song sitting in a verse instead of the chorus;
- a section that ends on a degree that is not the tonic and not the dominant (an unresolved ending);
- no short figure that returns (fragment: `brief` prints the Ins hook; if it "returns 0x", there is no hook to hum);
- a structural gap: the opening couplet never returns, the last line is never echoed;
- one clumsy spot (a leap with no preparation, a phrase that stalls).
Do not invent weaknesses. If the song is strong, the weaknesses are small (one cadence, one hook, one register
lift) — that is exactly the case where a light edit wins.

**(c) Signature gesture** — the one thing a listener would hum (a repeated-pitch recitation, a held high note, a
guitar figure that returns). Name it. All three variants keep it; at most one variant moves it.

### 2. Decide the maqam (due diligence)
```
python scripts/abc_tool.py maqam <song>/score.abc --label <Label>
```
Statuses: CONFIRMED (use the label), KEEP_LABEL (use the label, say so), OVERRIDE (use the tool's TARGET, state it
prominently), LOW_FIT (label, core notes only), NO_LABEL (TARGET). Read `TONIC UNSURE` / `CLOSE RIVALS` and decide
by where phrases rest and where the song ends. Record **(maqam, tonic)** and one sentence of evidence.
Read `references/maqam_rules.md` before touching a pitch.

### 3. Choose the three recipes
All three keep: maqam, tonic, `K:`, `L:`, section order, bar counts, the **meter scheme including mid-tune changes**,
the **chord track**, the source's tempo (±8% unless the recipe says otherwise), and the second voice's role.
Sung notes per section stay within 15% of the source (the words were sung over those notes).

| Variant | Idea | Keep | Change (this is the whole budget) | Floors |
|---|---|---|---|---|
| **A Enhance** | the same song, repaired | everything: melody, rhythm, meter, chords, register, accompaniment | 1-2 weaknesses only: one new 4-6 note hook figure in `Ins` that returns 3-4 times (**irregularly** spaced, in the gaps the voice leaves), one cadence repaired, one register lift in the chorus, one awkward leap smoothed. At most ~10% of the sung notes may move. | sim >= 0.75, rhythm >= 0.80 |
| **B Recompose one part** | one section written again, the rest untouched | intro, verses, interludes, outro, chords, meter, tempo | the weakest section (usually the chorus) is recomposed: new melody, but the same bars, the same note count, the same meter, the same rhythm character (median note length within x0.6-1.6) and the same chord track. It must fix the weakness that was named (e.g. lift the chorus a fourth). One new `Ins` line may answer it. | sim >= 0.55, rhythm >= 0.55 |
| **C New hook** | a new chorus hook plus what it needs | verses, structure, chords, tempo, mood, delivery | a genuinely new chorus melody and one new `Ins` counter-line that answers it; the verses keep their own melody and rhythm. This is the only variant allowed to surprise. | sim >= 0.40, rhythm >= 0.35 |

The three must differ **from each other in what they edit**: A changes the accompaniment and a cadence, B rewrites
one section, C writes a new chorus plus its answer. Because the untouched 80-90% dominates every global number, the
`verify` report lists the *sections that actually differ* (e.g. "3 (chorus), 6 (chorus)") — that is the useful line;
the whole-piece similarity beside it will be high in all three and is not a defect. Borrow a *behaviour* (e.g.
"answers every second line"), never retype a melody.

**What not to do**, in one line: do not smooth the rhythm, do not delete repeated notes, do not replace leaps with
steps, do not remove colour notes, do not flatten the meter, do not shrink the range, do not turn the second voice
into a filler, do not drop the chords. Each of those is a `FIX` from the tool, not a style choice.

### 4. Write the ABC
```
cp <song>/score.abc <song>/VAR_A_score.abc       # then edit bars in place
python scripts/abc_tool.py scale --maqam <Target> --tonic <Tonic> --key-from <song>/score.abc
```
- Follow `references/abc_writing.md`. Top of file: `% VARIANT A of <folder> | <Maqam> on <Tonic> | recipe: Enhance`.
- Keep `M:` changes exactly where the source has them, in **both** voices (and keep the bar count).
- Keep or add `% line N` comments so notes map to words. No `w:` lines. No quarter-tone reliance.
- If you wrote bars from scratch and dropped the chords, put them back:
  `python scripts/abc_tool.py chords-from <song>/score.abc VAR_A_score.abc` (it refuses to write if any note moves).
- Accidentals: write them on every affected note (see `native_dialect.md` §3).

Control (baseline for the listening test):
```
python scripts/abc_tool.py strip-chords <song>/score.abc <song>/CONTROL_score.abc
```
Never edit the control by hand; the command proves every note, onset, duration and the tempo is unchanged.

### 5. Validate and repair (up to 4 rounds per variant)
```
python scripts/abc_tool.py verify <song-folder> --maqam <Target> --tonic <Tonic>
```
It runs: bars, dialect, maqam, **fidelity + character + meter + chords**, layout parity, cadences, and the
distinctness between variants. Exit code 1 = `FIX` lines remain. Detail commands:
```
check / lint / modal                          (bars, dialect, maqam)
compare VAR_A_score.abc score.abc             (how much of the source survived)
features VAR_A_score.abc --tonic <Tonic>      (the numbers that must not collapse)
structure VAR_A_score.abc --tonic <Tonic>     (per-section register: did the chorus actually lift?)
```
**Fidelity floors** (from `fidelity_report`): melodic similarity, shared onset grid, repeated-pitch share, step/leap
balance, range, median note length, second-voice activity, meter scheme, chord presence. A `FIX` here means the
variant drifted too far — go back and edit *less*: start again from the source and change fewer bars.
`WARN` lines: fix if cheap, otherwise mention in the report.
- A `FIX` that survives 4 rounds: keep the file with `% UNRESOLVED: <what>` as its second line, list it in the report
  and index. A file that fails `check` (broken bars) is never delivered.

### 6. Write `VAR_REPORT.md`
Template: `references/report_template.md`. Short, simple Arabic. It must contain: the maqam decision and evidence;
the flavor card (**what we protected**); the weakness list and which variant fixes which; a table of the three
variants with *what changed* (be quantitative: "11 notes out of 394"), where to listen (bars), and one thing to
notice; the quality checks (fidelity numbers, meter kept, chords kept); assumptions; and the hypothesis each
variant tests. Under ~60 lines.

### 7. After the last song: `VARIANTS_INDEX.md` at the root
One row per song: folder, label, final maqam and tonic, status, anything unresolved; OVERRIDE / LOW_FIT /
TONIC UNSURE / UNRESOLVED cases first. End with `progress <root>`. Then a short chat summary (counts, exceptions)
and stop. No questions.

## Feedback sessions

He will name songs/variants and say what he heard, in a few words. Then:
1. Append to `FEEDBACK_LOG.md`: date, song, variant, recipe, his words, your interpretation (labelled hypothesis),
   decision. Factual and short.
2. **First question is always "too far or not far enough?"** If a generated track came out worse than the source,
   the seed was too different: go *closer* (higher fidelity, fewer edits), never bolder. If it came out identical
   and dull, go one step further on exactly one dimension.
3. Iterate **one change at a time** on the variant closest to what he wants: `VAR_B_score_r2.abc` (never overwrite),
   `% CHANGED` on the edited lines, re-run the validation loop, add a line to the report.
4. Look for patterns across songs (which recipe works per maqam, what he rejects) and write them in the log under
   "Patterns so far", low confidence until repeated. They become defaults for the next batch.
5. His explicit corrections about a maqam override `references/maqam_rules.md`; log and follow them.
6. **After three rounds without a "that's it" moment** on a song, say so and recommend generating several seeds and
   choosing by ear instead of more ABC edits.
7. If a variant feels right, give a generation brief: lyrics-tag edits, style-string edits, a best-of-N seed plan,
   and a rating note including the "shower test" (a day later, which version can he hum?).

## Round trip: scores that come back from generated tracks

1. Treat the returned score as a new source (`brief`, maybe `strip-chords`).
2. `compare` it against the variant that seeded it: the numbers say how much of the seed survived. One take, not
   proof that the seed steers the generator; log as a hypothesis next to his listening verdict.
   **If the returned track scores lower than the source, check the fidelity numbers first** — that is the usual cause.
3. A returned score that he likes better than the source becomes the new source (it enters the next batch).

## Honesty and scope

- Say "experiment" or "hypothesis", never "this will reach 9/10".
- The transcription misses guitars, strings, mix and melisma; its pitch accuracy is approximate. Changing a note that
  the transcriber merely guessed is not a real improvement.
- The thresholds in `abc_tool.py` (`RECIPES`, `OUT_FIX`, …) are starting values, calibrated on one song. He can run
  `survey <root>` on the corpus to see how labels and detection agree.
- Melody and structure sketching, not music-theory teaching unless he asks.
