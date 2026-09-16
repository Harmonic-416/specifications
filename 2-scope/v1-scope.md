# Scope

## In V1 (this semester)

**Theme: basic lessons + audio processing.** Everything else builds on these.

- **User auth** (server side).
- **Guided lesson path** — five- to ten-minute lessons on an unlocking,
  Duolingo-style map: explain the concept, drill it without the instrument, then
  play it.
- **Practice playlist** with **3 hardcoded songs**. Each song:
  - sheet music / tab display (tab + standard notation side by side);
  - reference-audio play button, toggleable during practice;
  - click or drag to a spot in the music to start playback there;
  - quick countdown, then live display of the note being sung / relative pitch
    against what's being played.
- **Voice sight-reading, guided mode (V1):** cursor doesn't advance until the right
  note is sung; 3 misses → auto-skip + recorded in score; manual skip; "hint" plays
  the note once; solfège toggle.
- **Voice sight-reading, practice mode (V2 of the interface, still this semester):**
  play straight through, post-run analysis of sung vs. score.
- **Guitar responsive tabs (audio only):** chord *verification* against the expected
  chord, chord cleanliness / "fuzziness" (not pressing hard enough, muted strings),
  tempo/timing, strumming pattern played vs. expected.
- **Guitar Learn mode (V1):** lesson holds on the current chord until verified, with a
  **soft gate** — after 3 attempts it advances anyway and records the result (a strict
  gate on imperfect detection is the Simply Guitar failure mode); manual skip always
  visible; hint plays the chord and shows finger positions.
- **Guitar Play mode (V1, second):** straight through at tempo, nothing stops you,
  post-run played-vs-score breakdown marked on the notation.
- **Tempo control** on the practice screen (50–100% of written tempo, persisted per
  song) — a verbatim competitor complaint is *"doesn't even let you choose the tempo."*
- **Lesson map supports knowledge-only nodes** (no mic needed) alongside play-along
  nodes — Lesson 1 is guitar anatomy, so a beginner reaches real instruction before
  our hardest technical problem can fail them.
- **Run-through summaries:** list of attempts, last score, recording included,
  clicking the music highlights patchy/spotty areas.
- **Built-in public-domain song library** + **MusicXML import** (we will *try* to
  support MuseScore and MIDI with file transformation — treat conversion beyond
  MusicXML as best-effort).
- **Dynamics detection** (volume up/down), **generated random melodies** for
  sight-reading, and **random chord progressions** from unlocked chords — if the audio
  pipeline lands early enough (these ride on the same foundation).

## Explicitly OUT of V1

| Cut | Why | Lands in |
|---|---|---|
| Computer vision (finger placement, fret mapping via camera) | Nontrivial calibration problem; stretch goal only | Stretch / V2+ |
| Group / social features (shared files, group sessions, collaborators, notes, multi-instrument songs) | Requires sync infrastructure; V1 is single-player | Future versions |
| Sheet-music-reading curriculum (full course) | V1 renders notation but doesn't teach it as a curriculum | Future versions |
| Advanced guitar techniques (slides, bends, hammer-ons, pull-offs) | V1 covers chords/strumming basics only | Future versions |
| Guitar "Changes" mode (two chords alternating, scored on clean changes) | Depends on the gate + timing score working first (F38) | Next version |
| Full-song playthroughs | V1 is lesson- and practice-piece-scale | Future versions |
| YouTube play-along scoring | Depends on timing/sync work beyond V1 | Future versions |
| Piano | Deck vision includes it; semester scope is guitar + voice | Future versions |
| App Store release | $99 TestFlight question unresolved; PWA may sidestep it | TBD |

## Won't do (any version, current thinking)

- Song-first gamification without theory — that's the competitor failure mode we're
  defined against (see [problem.md](../1-problem-and-users/problem.md)).

## Risks that could shrink this scope

See [potential-problems.md](potential-problems.md). The single biggest unknown:
real-time pitch detection working **on a phone in Safari**. If it doesn't, scope
shifts toward desktop-first.
