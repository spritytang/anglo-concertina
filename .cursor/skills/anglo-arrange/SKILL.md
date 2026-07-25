---
name: anglo-arrange
description: >-
  Arrange tunes for 30-button C/G Anglo concertina (Wheatstone / Wren 2):
  verify melody against a locked source before any fingering, fit same-direction
  left-hand harmony, then optimize cross-row fingering. Use when the user asks
  to 扒谱, tab, arrange, finger, add LH chords/伴奏, reduce 推拉换向, or edit
  Fly Me / 小白猫 / tunes / bellows lessons in the Music Anglo site.
---

# Anglo Arrange (C/G · Wheatstone · Wren 2)

Follow this skill + project rules `anglo-arrangement.mdc` and `jianpu-notation.mdc`. Prefer published / user-given sources over memory.

## Hard constraints

1. **Pitch first** — never change melody notes/octaves only to save bellows flips.
2. **Same bellows for RH+LH** — Anglo cannot mix push and pull in one chord/hit.
3. **Board orientation** — always **左手 Left on screen-left**, **右手 Right on screen-right** (player holding the box). Never swap sides when `focusSide` is set.
4. **Wren 2 corner octaves** (verified on user's box):
   - RH top-right **pull** = **F6** (`f'''`), not F7
   - RH bottom-right **pull** = **♯F6** (`f#'''`), not ♯F7
5. Edit only `index.html`, then `cp index.html anglo-intro.html`.

---

## Melody correctness (mandatory — do this every time)

Wrong melody has already shipped once (Fly Me dumbed-down contour). **Do not ship pitch from song title or memory alone.**

### Arrange progress

```
Arrange progress:
- [ ] 1. Lock melody SOURCE (user 简谱 / lead sheet / timestamped video / Real Book)
- [ ] 2. Normalize to degree string + octave (C=1 … B=7; write holds separately)
- [ ] 3. Store `sourceDegrees` next to the song data (e.g. KOSHKA.A.sourceDegrees)
- [ ] 4. Map letters → steps; regenerate degree string FROM steps
- [ ] 5. Diff: sourceDegrees === degreesFromSteps (must match exactly)
- [ ] 6. Spot-check disputed phrases with user lyrics (syllable ↔ pitch)
- [ ] 7. Only then: RH fingering → LH same-dir → bellows count
- [ ] 8. Site checks: array lengths; createPeriodicWave still present
```

### How to lock the source

| User gave… | Treat as truth |
|------------|----------------|
| 简谱串如 `3-5-6-676-5-3---` | Parse digits in order; `-` after a note = sustain (beats), not a pitch |
| Staff / ABC / Real Book | Extract pitch sequence in the stated key |
| “听起来像 X” without pitches | **Ask** for 简谱 or a link before arranging |
| Only a title | **Ask** — do not invent |

### Degree check (run before saying done)

From each melody step’s ABC note in C major / relative Am:

```
c→1  d→2  e→3  f→4  g→5  a→6  b→7
(ignore octave marks for the degree string unless the source marked 高/低音)
```

Example — 小白猫 user source:

```
source: 3-5-6-676-5-3---21-6-2-232-1-2-
digits: 35667653216223212
```

If `steps.map(solf).join("")` ≠ that string, **stop and fix pitches** before fingering polish.

### Known locked sources in this repo

| Song | Panel | Locked degree string (opening / current section) |
|------|-------|--------------------------------------------------|
| Belaya Koshka | `#koshka` | `35667653216223212` |
| Fly Me to the Moon | `#flyme` | User/lead-sheet contour; opening **high C–B–A–G–F** (not `CCCF…`) |

When editing these songs, re-run the degree check. If the user supplies a new 简谱, update `sourceDegrees` and the steps together in one change.

---

## Workflow after melody is locked

### Chords (harmonic / English style)

- Melody RH, chords LH; **direction follows the melody**.
- No matching-dir triad → substitute (Em push ↔ Am pull) or drop a tone — never reverse bellows only for LH.

### RH / bellows economy

| Pitch | Prefer when… | Layout |
|------|----------------|--------|
| G pull | pull run | top② `g''` |
| A push | push run | top② `a''` |
| B push | push run | bot② |
| C high pull | pull run | bot③ `c'''` |
| E `e''` pull | pull run (keep octave) | **LH bot⑤ pull** (`y` in Fly Me) |
| F `f''` | pull only on RH | mid③ pull |

- **F↔E on RH alone ⇒ mandatory flip**; same-octave pull E uses **left** `e''`.
- Forbid empty flips (push G then immediately pull same G).

### Site checks

- Letter / lyric / chord / beat array lengths match.
- Jianpu accidentals stay on the same line as the degree (`.jp-deg`).
- Mobile: `unlockAudio` before play sequences.
- After audio edits: `grep createPeriodicWave index.html`.

## Output

Brief: **source** · **degree string (before/after check)** · chords · flip notes · assumptions.

## Deeper reference

See [reference.md](reference.md).
