# Requirements

MoSCoW priorities: **M** = must (V1 fails without it), **S** = should,
**C** = could (if time allows), **W** = won't (this semester).

## Functional requirements

### Accounts & lessons
| # | Requirement | Priority |
|---|---|---|
| F1 | Users can register, log in, and have per-user progress stored | M |
| F2 | Lessons are arranged on an unlocking map; a node unlocks when prerequisites are cleared | M |
| F3 | Each lesson: concept explanation → instrument-free drill → played exercise | M |

### Practice pieces
| # | Requirement | Priority |
|---|---|---|
| F4 | Playlist of practice pieces; V1 ships 3 hardcoded songs | M |
| F5 | Tab and standard notation rendered side by side | M |
| F6 | Reference audio playback, toggleable during practice | M |
| F7 | Click/drag anywhere in the music to start playback from that point | S |
| F8 | Countdown before a practice run starts | S |
| F9 | MusicXML import of user scores | S |
| F10 | MuseScore/MIDI file transformation | C |

### Listening & scoring
| # | Requirement | Priority |
|---|---|---|
| F11 | Real-time mic pitch detection; each note scored hit / late / missed | M |
| F12 | Live display of the sung note or relative pitch vs. the expected note | M |
| F13 | Guided mode (instrument-neutral): doesn't advance until the expected note/chord is verified; 3 misses → auto-skip recorded in score; manual skip; "hint" plays the expected note/chord once. Guitar-specific gate behavior in F28–F31 | M |
| F14 | Practice/play mode (instrument-neutral): uninterrupted play-through with post-run performed-vs-score analysis. Guitar specifics in F32–F33 | S |
| F15 | Notation label toggle (instrument-neutral): solfège for voice; frets / note names / finger numbers on guitar chord diagrams (F35) | S |
| F16 | Guitar: chord **verification** while held — does the audio match the one expected chord (not arbitrary-chord recognition) | M |
| F17 | Guitar: chord cleanliness ("fuzziness" — under-pressed / muted strings) | S |
| F18 | Guitar: strumming pattern played vs. expected; timing/tempo score | S |
| F19 | Dynamics detection (volume rising/falling) | C |
| F20 | Random exercise generation (instrument-neutral): melodies for voice sight-reading; chord progressions for guitar (F36) | C |
| F21 | Explicit "couldn't hear you" state when input is too quiet to score | M |

### Guitar practice modes (adopted from [guitar-learning-path.md](../1-problem-and-users/guitar-learning-path.md))
| # | Requirement | Priority |
|---|---|---|
| F28 | Guitar guided ("Learn") mode: lesson holds on the current chord until verified; **soft gate** — advances after N attempts (N=3) rather than blocking indefinitely | M |
| F29 | Three misses → auto-skip, recorded in score; a miss is a failed strum **or** a silence timeout with no strum onset | M |
| F30 | Manual skip / override, always visible during a lesson | M |
| F31 | Hint: play the chord once through the reference synth **and** animate the finger positions onto the fretboard diagram | S |
| F32 | Guitar "Play" mode: uninterrupted run at tempo, no gating | S |
| F33 | Post-run played-vs-score analysis — per chord: verified / wrong / not heard, and early / on / late — marked on the notation | S |
| F34 | Live chord state during a run (expected / heard something else / heard nothing). Per-string indicators depend on F17 | S |
| F35 | Chord-diagram label toggle: fret numbers, note names, or finger numbers | S |
| F36 | Random chord-progression generation from unlocked chords, at a chosen tempo | C |
| F37 | Tempo control on the practice screen, 50–100% of written tempo, persisted per song | M |
| F38 | "Changes" mode: two chords alternating at a user-set tempo, ungated, scored on clean changes per window (depends on F28 + F18) | W (next version) |

### Review
| # | Requirement | Priority |
|---|---|---|
| F22 | Run-through history per song, with last score | M |
| F23 | Recording of each attempt attached to its summary | S |
| F24 | Clicking the music in a summary highlights patchy/spotty areas | S |

### Won't (this semester)
| # | Requirement | Priority |
|---|---|---|
| F25 | Computer-vision finger-placement feedback | W (stretch) |
| F26 | Group sessions / collaborators / shared files / multi-instrument songs | W |
| F27 | YouTube play-along scoring | W |

## Non-functional requirements

| # | Requirement | Priority |
|---|---|---|
| N1 | Pitch-detection latency low enough for note-by-note feedback (target ≲100 ms mic-to-score; measure early) | M |
| N2 | Works on a real phone in mobile Safari — validate before building on top | M |
| N3 | Audio data compressed for storage/transfer (recordings, analysis data) | S |
| N4 | Offline/cached practice content if we go PWA (service worker) | C |
| N5 | User recordings are private to the user by default | M |
| N6 | Graceful behavior under background noise (reject, don't mis-score) | S |
