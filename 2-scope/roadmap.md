# Roadmap — four versions

The semester scope ([v1-scope.md](v1-scope.md)) split into four ~3-week milestones.
Each one is a **demoable vertical slice**, ordered so the biggest risk dies first
(real-time pitch detection on a phone in Safari — see
[potential-problems.md](potential-problems.md)), and so each instrument gets a
dedicated version: voice (monophonic, simpler) before guitar (polyphonic, custom
detection). Requirement numbers reference [requirements.md](requirements.md).

| Version | Target | Theme |
|---|---|---|
| **v1** | ~Oct 7 | Prove the audio pipeline + app skeleton |
| **v2** | ~Oct 28 | Voice: complete practice & review loop |
| **v3** | ~Nov 18 | Guitar: chords, strumming, cleanliness |
| **v4** | ~Dec 15 (demo) | Lessons, import, polish, stretch items |

## v1 — "It hears you" (early October)

Goal: kill the technical unknowns and stand up the skeleton everything else builds on.
If mobile-Safari pitch detection fails here, we still have time to pivot desktop-first.

- **Pitch-detection spike on a real phone in Safari** — measured mic-to-score
  latency vs. the ≲100 ms target (N1, N2). Go/no-go written up.
- App shell on the decided stack (React + Vite PWA, Supabase for auth/DB/storage —
  see [tech-stack-2.md](../3-architecture/tech-stack-2.md)): navigation, auth +
  per-user progress storage (F1).
- Onboarding sound check: mic permission → live level meter → "play any string" —
  the first proof detection works on the user's device; tuner rides on this.
- Song display: tab + standard notation side by side (F5), reference-audio
  playback toggle (F6), for at least **1 hardcoded song**.
- Live pitch display: sung note / relative pitch vs. expected note (F11, F12),
  including the "couldn't hear you" state (F21).
- **Demo:** log in, open a song, sing at the phone, watch it track you live.

## v2 — "The voice loop" (late October)

Goal: a singer can practice a song end to end and review how it went.

- **Guided mode** complete: cursor waits for the right note, 3 misses →
  auto-skip recorded in score, manual skip, hint plays the note (F13); solfège
  toggle (F15).
- **Practice mode**: uninterrupted play-through + post-run sung-vs-score
  analysis (F14).
- All **3 hardcoded songs** in the playlist (F4); click/drag-to-seek (F7);
  countdown (F8); tempo control 50–100%, persisted per song (F37).
- Run-through history with last score (F22); attempt recordings attached (F23).
- Background-noise handling: reject, don't mis-score (N6).
- **Demo:** full guided + practice runs on voice, then open the summary.

## v3 — "The guitar loop" (mid-November)

Goal: the same loop works for guitar — the harder detection problem, built on a
pipeline v2 has already proven.

- Chord **verification** while held — match against the one expected chord, a
  handful of open chords, not the fretboard (F16).
- **Learn mode** with the soft gate: hold until verified, advance after 3 attempts,
  auto-skip recorded, manual skip, hint plays + shows the chord (F28–F31).
- **Play mode**: uninterrupted run + post-run played-vs-score marked on the
  notation (F32–F33); live chord state during a run (F34).
- Strumming pattern played vs. expected; timing/tempo score (F18).
- Chord cleanliness / "fuzziness" — muted strings, under-pressing (F17); per-string
  indicators in F34 depend on this landing.
- Chord-diagram label toggle: frets / notes / fingers (F35).
- Guitar songs wired into the same playlist, summaries, and recordings flow.
- Summary click-to-highlight patchy/spotty areas (F24) — now that both
  instruments produce per-note scores.
- **Demo:** full practice run on guitar with chord-quality feedback, then
  review patchy areas in the summary.

## v4 — "Teach the language" (semester end)

Goal: the theory-first layer that differentiates us, plus content flexibility
and polish.

- Guided lesson path on the unlocking map: concept → instrument-free drill →
  played exercise (F2, F3), including **knowledge-only nodes** — Lesson 1 "Meet the
  guitar" and Lesson 2 "E minor" from
  [guitar-learning-path.md](../1-problem-and-users/guitar-learning-path.md).
- MusicXML import (F9); MuseScore/MIDI conversion best-effort (F10).
- Audio compression for recordings/analysis data (N3).
- **If time (C-priority):** dynamics detection (F19), random sight-reading
  melodies / chord progressions (F20, F36), offline/cached practice content (N4).
  Guitar "Changes" mode (F38) stays next-version.
- **Demo (final):** new user works through a lesson node, unlocks a song,
  practices it on either instrument, imports their own MusicXML.

## Slip rules

If a version slips, cut from the bottom of that version's list (C's before S's
before M's), never by pushing the pitch-detection spike later — it gates
everything. If guitar detection (v3) proves harder than planned, chord identity
(F16, an M) survives and fuzziness/strumming (F17/F18, S's) shrink — the lesson
layer (v4) doesn't move, since it doesn't depend on them. Computer vision,
social features, and piano stay out entirely (see [v1-scope.md](v1-scope.md)).
