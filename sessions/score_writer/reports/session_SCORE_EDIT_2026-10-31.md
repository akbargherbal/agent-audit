# Audit — `sessions/score_writer/session_SCORE_EDIT.json`

- **Log format:** Google AI Studio export; `chunkedPrompt.chunks[]` with text / `isThought` /
  `executableCode` / `inlineFile`. Turns cited as **chunk N**; input lines as `input/e01_base.txt:N`.
- **No prior report** (`reports/` held only `.gitkeep`). **No `expected.md`** — correctness is judged
  against SKILL.md and the score itself.
- **The only score given is `e01_base.txt`**, and its own header says it is a previous variant
  (`:9` = `% VARIANT A of 04-… | Nahawand on D# | recipe: Polish`). There is no `score.abc`.

---

## 1. Summary

**Task (chunk 3):** "عدل على السكور … e01_base.txt أعطني الثلاث variants للسكور" — write VAR_A /
VAR_B / VAR_C from `e01_base.txt` under the attached SKILL.md, lyrics and references.

**Outcome:** three variants, a control and a 48-line Arabic report. All files are valid ABC: 124 bars in
each voice, every bar 16 units, header / `M:2/4` / `L:1/32` / `Q:1/4=65` / `K:D#m` preserved, section
comments kept, no forbidden tokens, every note inside the Nahawand-on-D# pitch set.

**Correct?** *Mechanically yes; musically, only C is defensible.*
- **A** does the four things the skill forbids: it smooths a leap, deletes a breath, replaces a held
  note with a run, and changes a chorus cadence — in both choruses.
- **B** recomposes the chorus into a **flatter** chorus than the source: leaps 14.6% → 1.5%, steps
  82.1% → 93.1%, apex unchanged. That is the "cleaner, tidier" rewrite the skill exists to prevent.
- **C** is the only variant that moves toward the documented source profile: repeated pitches
  3.3% → 13.8%, `Ins` sounding in the chorus 0% → 15.6%.
- The named weakness "the chorus has low energy" is not supported by the numbers: the source chorus
  already has the song's highest note (77) and a higher mean than the verse (69.2 vs 66.9).
- The input is itself a flattened variant, and the report protects the flattened numbers (86.4%
  stepwise, 3.9% repetition) as identity instead of naming them as damage.

**Size:** 135 chunks, 46 code executions, three variants + control + report.

---

## 2. Progress since last report

None — first report on this session.

---

## 3. Minimal path

1. **Read the source and its header.** Decide what the file is (a prior variant) and which profile you
   are repairing toward. Write that decision down.
2. **Map the phrases.** For every sung line: start degree, apex, landing degree, breath after the last
   note. This map is the contract for every later edit.
3. **Map the sections.** Mean/max pitch, note count, `Ins` sounding share, cadence behaviour. This is
   what a weakness must cite.
4. **Name 2–3 weaknesses with numbers**, and reject any claim the section map contradicts (e.g. "low
   chorus energy" when the chorus holds the song's apex).
5. **Give each variant one dimension.** A: an `Ins` line + one named cadence. B: one section
   occurrence, recomposed. C: a new hook + its `Ins` answer.
6. **Write at phrase level**, preserving start, apex, landing and breath unless the weakness names one
   of them.
7. **Diff the invariants and the character numbers** (leap %, repetition %, apex, `Ins` share,
   degree mix). If a leap share collapses or a landing moves, the rewrite failed — rewrite it again.
8. **Report what changed and where to listen**, not that it "sounds better".

---

## 4. Deviations

| # | Step | What happened | Cause | Proposed fix | Impact |
|---|---|---|---|---|---|
| M1 | A, verse 14–15 | `E2F2G4F2E6\|A8z8` → `E2F2G4F2E4F2\|G2F2E4D8`: the E→A fourth is filled with F and the 8-unit breath after the held A is deleted. The thinking says "inserting an F2 to connect the notes" (chunk 71). | The weakness was framed as "an unprepared leap", so the fix removed the leap. | Prepare the leap *before* it and keep the held A and its breath. Smoothing a leap is a `FIX`, not a repair. | Deletes a signature gesture and a deliberate breath — the exact flattening the skill warns about. |
| M2 | A, chorus 56–57 and 103–104 | `…d2c2B4A8\|E8D8` (held 5, then 2→1) → `…A4c4\|B4A4F2E2D4`. The held 5 is gone and the 2→1 descent is replaced by a run. Done in **both** choruses. | No cadence map; the edit was made note-by-note. | Diff each phrase's landing degree; a changed landing is allowed only when the named weakness *is* that cadence. | Changes the chorus closure and the phrase's resting point; the report does not mention it. |
| M3 | A, `Ins` | The "chorus has no Ins" weakness is "fixed" with one 5-note cell in the final `D16` bar of each chorus: 24 sounding units of 1024 (2.3%). Two of the six placements also overwrite existing source fills (verse 10, 30). | "Add a hook" was read as "put notes in the rests". | `Ins` is a line: one continuous 2–4 bar counter-melody per section, sounding share within ±5 points of the source. | The chorus body is still silent; the arrangement problem is not solved. |
| M4 | A, hook | Three different 5-note cells, each used twice (`D2E2F2E2`, `D2c2B2A2`, `F2G2A2c2d4`), not one figure returning 3–4 times. | No motif discipline. | One 4–6 note cell, 3–4 irregular placements, varied by inversion/transposition. | Nothing is recognisable as "the hook"; it reads as three fills. |
| M5 | B, chorus | Recomposed chorus is smoother than the source: leaps **14.6% → 1.5%**, steps **82.1% → 93.1%**, repeated pitches 3.3% → 5.4%. | A stepwise "safe" melody; only median note length was checked (it stayed 0.462 s). | Character floors on the rewritten section: leap share ±4 points, repetition ±5 points, apex not lower. | B is the flattening failure the skill describes, sold as "recompose". |
| M6 | B, "lift" | Mean rises 69.2 → 71.5 (+2.3 semitones) but the apex stays 77 in all versions. | No before/after register measurement. | "Lift" must name a mean or apex interval and print both. | The claimed lift is a shade, not a lift. |
| M7 | Weakness #3 | "Low chorus energy / no climax" — the source chorus already has the highest mean (69.2 vs verse 66.9) and the song's highest note (77). | No per-section register check; the claim came from reading the melody. | Every "low energy" claim must cite mean and max next to the previous section. | B spends its whole budget solving a non-problem. |
| M8 | B and C, colour | b7 goes 2.3% → 7.6% in both (3.3×). The report presents it as fixing "rare b7". | "More colour = better" instead of matching the source mix. | Match each degree within ±2 points of the source; colour is matched, not maximised. | A different Nahawand colour, not the song's. |
| M9 | B and C, scope | Both replace the same 30 vocal bars (chorus 1 bars 1–8, chorus 2 bars 1–22); B-vs-C pitch similarity 0.807 (chunk 114). | The recipe table is ambiguous; no distinctness check. | B replaces **one** occurrence; C writes the hook and its answer. | Three variants, two experiments. |
| M10 | B and C, cadence | Both turn the chorus's first phrase from a tonic landing (source `D8E4D4`, degree 1) into a dominant landing (`A8G4A4` / `c6B2A8`, degree 5). | Phrase landings were never mapped. | Keep the source's landing unless the weakness names it; if you open the phrase on 5 deliberately, say so. | The chorus no longer closes its first line the way the song does. |
| M11 | B and C, prosody | C sets 19 notes on the chorus line (~13 syllables); B sets 16. No syllable count was made, although the lyrics were attached. | The lyrics were read for theme only (chunk 17). | Count notes per syllable in every rewritten phrase; flag >1.5 and say whether it is melisma. | Risk that the line no longer fits the words it was sung to. |
| M12 | Source / report | Input header says it is a prior variant; its numbers match the skill's "flattened" column on 5 of 7 rows (0.462 s / 3.9% / 86.4% / 2.3% / no chords / `M:2/4` only). The report instead protects 86.4% stepwise as identity. | No provenance step; flavor card built from absolute numbers only. | Check the header and the damage table before choosing what to protect; state the target profile. | The variants entrench the damage the skill was written to repair. |
| M13 | Harmony | Source has no chord symbols; the report calls it "chord-free and ready for generation". Per the skill, the source had a chord track (138 symbols in the reference) and losing it is damage. | No harmony step. | Restore chords from the original, or state that the seed has lost its harmony; do not present a chordless score as a property. | The generator receives no harmony; abcjs plays a bare melody. |
| M14 | Modal accuracy | "In the maqam" was checked only as pitch-set membership (all notes in 0 2 3 5 7 8 10). No sayr, cadence or degree-mix check; `CONFIRMED` is asserted. | Scale membership was treated as modal compliance. | Check the 2↔b3 pair, the cadence formulas, and the degree mix; say "in scale" when that is all you checked. | "In scale" is not "in maqam"; the report overstates modal accuracy. |

---

## 5. Ranked edits

Ordered by musical impact. Exact replacement text for `SKILL.md`; `G` = generalizable.

### E1 — Phrase map and invariants (G)
Add before step 4 ("Write the ABC"):

```
Before writing a bar, list every phrase as (start degree, apex, landing degree, breath after the last
note). After writing, diff the list. A changed landing or a deleted breath is allowed only if the named
weakness is that cadence or that breath; otherwise restore it.
```

### E2 — Forbidden edits for A (G)
Replace the "What not to do" line in step 3 with:

```
For A these are never repairs: replacing a held note with a run, filling a breath that is part of the
delivery, smoothing a leap (prepare it before the leap instead), and changing a phrase's landing degree.
If your fix removes the thing you named as a weakness, you removed a quirk, not a fault.
```

### E3 — Character floors for B and C (G)
Add to the variant table in step 3:

```
B and C floors, measured on the rewritten section only: leap share within ±4 points of the source
section, repeated-pitch share within ±5 points, apex not lower, median note length within x0.6-1.6.
A recomposition that turns 14.6% leaps into 1.5% is a FIX, not a new chorus.
```

### E4 — `Ins` is a line (G)
Add to step 4 and to `references/abc_writing.md` §8:

```
Ins is a line: at least one continuous 2-4 bar counter-melody per section, sounding share within
±5 points of the source section. Four-note cells dropped into rests are fills, not a second voice;
they do not fix "the chorus has no Ins".
```

### E5 — Provenance and target profile (G)
Add as step 0:

```
Read the first 12 lines. `% VARIANT ... | recipe: ...` means the file is a previous variant. Compare
its numbers with the damage table: if two or more match the "flattened" column, say so and repair
toward the source profile, not toward the file's numbers.
```

### E6 — Measure the lift (G)
Add to the B row in step 3:

```
"Lift the chorus" means a named interval in mean or apex, printed before/after. Raising the mean by
2 semitones while the apex stays the same is a shade, not a lift; say which one you did.
```

### E7 — Degree-mix band (G)
Add to step 1(a) and `references/maqam_rules.md` §8:

```
Match the source's degree mix within ±2 points per degree (b7 2.3% -> 7.6% is a different colour,
not a repair). Colour is matched, not maximised.
```

### E8 — Prosody check (G)
Add to step 4:

```
Count notes per lyric syllable in every rewritten phrase. Flag above 1.5 notes/syllable and say why
(melisma, or a phrase that no longer fits the line).
```

### E9 — One experiment per variant (G)
Replace the distinctness paragraph in step 3:

```
B replaces one section occurrence and leaves the other untouched; C writes the hook and its answer.
If both replace the same bars, you tested one hypothesis twice.
```

### E10 — Harmony is part of the seed (G)
Add to step 4:

```
A chordless source is a lost chord track, not a property. Restore it from the original or say the
seed has no harmony; do not call a chordless score "ready for generation".
```

---

## 6. Overfit vs generalizable

**Run-specific**
- The exact bars (14–15, 56–57, 103–104), the three hook cells, and the D#m/Nahawand spelling.
- The `e01_base` provenance conclusion (a prior "Polish" variant) — but the check for it is general.

**Generalizable**
- Rewrite at phrase level and diff landing / apex / breath, not just note counts (M1, M2, M10).
- A "repair" that removes a leap, a held note or a breath is damage (M1, M2).
- Measure character (leap %, repetition %, apex) on the rewritten section; stepwise safety is flattening (M5).
- `Ins` must be a line, not cells in rests (M3, M4).
- A lift must move the apex or be stated as a mean shift (M6).
- Weaknesses must be supported by per-section mean/max, not by reading (M7).
- Match the source's degree mix instead of maximising colour (M8).
- Check whether the input is already a variant before protecting its numbers (M12).
- A chordless seed has lost its harmony (M13).
- "In scale" is not "in maqam": check cadence and sayr (M14).

---

## 7. Open questions / assumptions

1. **Is `e01_base.txt` the 8/10 source or the flattened 6.5 variant?** The header says it is a variant
   with a "Polish" recipe (not one of the current three), and its numbers match the damage column on 5
   of 7 rows. But `…_time.txt` shows this same file was the `abc_file` seed for the generated track
   (`--request-option abc_file=…/e01_base.abc --seed 2020610301`), so the user may have been rating
   *this* profile. Either way the report had to say which; it says neither. I treat the "flattened
   variant" reading as more likely because of the header.
2. **No original `score.abc`** — the chord track and the pre-flattening melody are unavailable, so the
   identity target can only be described, not restored. Assumed when judging M12/M13.
3. **The "weak chorus" premise** may come from the user's ear rather than the numbers. If he hears it as
   weak despite the chorus holding the apex, that is a valid ear judgment — but it must be stated as
   such, not as a measured weakness.
4. **Whether B's smoother chorus is preferable** is a listening question; the skill's own damage table
   says a stepwise chorus is the failure mode, so B is judged against that, not against taste.
