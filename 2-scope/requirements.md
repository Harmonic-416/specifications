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
| F13 | Guided mode: cursor doesn't advance until the correct note; 3 misses → auto-skip recorded in score; manual skip; "hint" plays the note once | M |
| F14 | Practice mode: uninterrupted play-through with post-run sung-vs-score analysis | S |
| F15 | Solfège labels toggle on/off | S |
| F16 | Guitar: chord identity check while held | M |
| F17 | Guitar: chord cleanliness ("fuzziness" — under-pressed / muted strings) | S |
| F18 | Guitar: strumming pattern played vs. expected; timing/tempo score | S |
| F19 | Dynamics detection (volume rising/falling) | C |
| F20 | Random melody generation for sight-reading | C |
| F21 | Explicit "couldn't hear you" state when input is too quiet to score | M |

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
