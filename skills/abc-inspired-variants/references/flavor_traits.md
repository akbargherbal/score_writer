# Flavor traits: from numbers to plain Arabic to ABC

Use this to build the flavor card for each reference score (SKILL.md step 1) and to decide what a variant must
**protect**. The traits below are what makes the song itself: a variant may amplify one of them deliberately, never
delete one by accident. The numbers come from `python scripts/abc_tool.py features file.abc`; `python scripts/abc_tool.py traits file.abc` compares one song with its sibling songs in the same folder and prints the 5 most unusual numbers (z-scores), which is the fastest route to the flavor card. Use `--tonic <Tonic>` on `features` with the tonic decided in step 2, because the `K:` line is only a guess and the `degrees_pct` row is measured from it.

## Contents
1. Trait table
2. Picking the distinctive traits
3. Realizing each trait in ABC
4. Making a hook (hypotheses to test, not rules)
5. Translating for the user

## 1. Trait table

| Number from `features` | What it says | Plain-Arabic hint |
|---|---|---|
| `avg_notes_per_phrase`, `avg_phrase_sec` | long phrase = reads like recitation; short phrase = singable | "الجملة طويلة كأنها إلقاء" / "الجملة قصيرة وتُغنّى" |
| `repeated_pitch_pct` | share of notes that stay on the same pitch (recitation feel) | "اللحن يقف على نغمة واحدة كثيرًا" |
| `step_pct` / `leap_pct` | smooth stepwise motion vs jumps | "حركة هادئة متدرجة" / "قفزات" |
| `notes_per_sec_when_sounding`, `median_note_sec` | rhythmic busyness. Comparable across files, unlike raw note units | "إيقاع كثيف" / "نغمات ممتدة" |
| `sounding_pct` (Vocal) | how much silence the singer leaves | "مساحات صمت" |
| `range_semitones` | how high/low the line travels (12 = one octave) | "مدى واسع" |
| `degrees_pct` | which notes of the scale are the home notes; "1" is home, "5" the dominant, "b2" a lowered second (Kurd/Hijaz color), "b6"/"b7" minor color | "النغمة التي يدور حولها اللحن" |
| `similar_phrase_pairs` | how many phrase pairs are 70%+ alike (melodic repetition) | "جمل تتكرر" |
| `most_repeated_5_interval_pattern` | the most repeated 5-move pattern (often five equal notes = recitation) | |
| `short_groups`, `short_group_gap_sec` | short answers (<= 9 notes) after a gap: instrumental fills or sung tags, with their time stamps and spacing | "ردود قصيرة من الغيتار" |
| `longest_evenly_spaced_run_of_fills` | how many fills in a row are spaced almost equally (+-25%). High = mechanical | "تأتي كالساعة" |
| `distinct_short_shapes` | how many different fill shapes exist. 1-3 = a signature; 10+ = many unrelated tags | |
| `fills_per_min` (only in `traits`) | `short_groups` per minute | "كم ردًّا قصيرًا في الدقيقة" |
| `length_sec` | song length | |
| Ins `sounding_pct` | how much the accompaniment line speaks at all | |

Caveats: the transcriber guesses tempo and meter each time, so use per-second and per-phrase numbers; the key signature says nothing reliable about the maqam; Ins coverage is partial, so a missing fill may just be a transcription miss.

## 2. Picking the distinctive traits

In autonomous runs there are no words from the user about why he likes a song. Use `traits`: the traits
with |z| >= 1 against the siblings in the same maqam folder are that song's flavor; take the top two or
three. If nothing reaches |z| >= 1, say the song is statistically ordinary for its folder and rely on the recipes' structural
ideas instead. Mention in the report that the flavor card is read from numbers only.
When he later gives his own words about a song (feedback session), his words win over the numbers.

## 3. Protecting a trait (default) or amplifying it (deliberately)

Every bullet has two columns of thought: the first line is **how to keep this trait** in an edit; the second is when
you may push it further.

- **Long recitation-like phrases** (`avg_notes_per_phrase` high, `repeated_pitch_pct` high): this is how a long
  classical hemistich is actually sung. Keep the repeated notes and the long phrases. Only B (Recompose) may cut one
  section into shorter chunks, and only if "the line is shapeless" is on the weakness list.
- **Short singable phrases**: keep the rests where the source has them; you may add one breath before a cadence.
- **Smooth steps vs leaps** (`step_pct`/`leap_pct`): copy the ratio. If the source leaps on 16% of its moves, a new
  section should leap on roughly 16%, not on 5%. Leaps are where the drama lives.
- **Rhythmic busyness** (`median_note_sec`, `notes_per_sec_when_sounding`): any new material must land within
  x0.6-1.6 of the source's median note length. Doubling the note length is heard as "slower and sleepier".
- **Silence** (`sounding_pct`): keep the source's share. Filling every gap with a fill is a downgrade.
- **The second voice** (`Ins` sounding_pct, note count, range): it is an arrangement line. Keep its activity level and
  its span; a counter-melody is allowed, four 3-note fills are not.
- **Mode colour** (`degrees_pct`): keep the mix. Losing b7 in Nahawand or 6 in Hijaz strips the colour he liked.
- **Range and contour**: keep the source's apex where it is. Moving the highest note from the verse into the chorus is
  a *great* weakness to fix (that is B's job); compressing the whole melody into one octave is not.
- **Refrain**: if the source already repeats a couplet (intro/verse/chorus), keep the repeat. Adding one is a
  structural improvement worth testing in B or C.
- **Fills**: keep the ones the source has, in the same places. A new fill may be added only in A (the hook) or to
  answer a recomposed section in B/C.

## 4. Making a hook (hypotheses to test, not rules)

From the project's tracks (see `project_context.md`, section 4): a short figure of 4-8 notes with a distinctive
rhythm; placed in the silence after a sung line; recurring with small variation at less predictable intervals;
present early so the ear can latch on. **Build it from the source's own material** (a fragment of its intro, its
chorus tail, or its own fill) rather than inventing a new motif: a hook the listener half-knows already is the
cheapest improvement available. Offer it as an experiment; if he reacts against it, drop it.

## 5. Translating for the user

- One sentence per trait, in plain Arabic, with a concrete picture ("الغيتار يرد على الصوت بعد كل بيت").
- Tie a trait to his own words about the song when he gave any; in autonomous runs there are none, so say the trait comes from the numbers.
- Explain a term once and then reuse it: `phrase` = جملة، `fill` = لزمة قصيرة تملأ الفراغ، `hook` = اللزمة التي تلتصق بالذاكرة، `bar` = مقطع زمني قصير يفصله خط عمودي.
