# Tech Stack

## Open decision: Flutter vs. web PWA

Two directions are on the table and we need to pick one:

- **Flutter / Dart** — cross-platform native app.
- **Plain-web / JS PWA** — fits the team's shared skillset, and the entire library
  list below assumes this stack.

> Implementation note: whichever we pick, build and test the pitch-detection pipeline
> **on an actual phone in Safari** before committing further — that's the biggest
> unknown, regardless of which UI framework sits on top.

## Library list (web/JS stack), by feature

### Notation & tab rendering

| Library | Use |
|---|---|
| **AlphaTab** | The core pick. Cross-platform music notation and guitar tablature rendering; loads Guitar Pro, its own AlphaTex markup, or MusicXML, and renders standard notation and tabs in the browser. Built-in MIDI synth for playback, so it can double as the "reference audio" player. |
| **VexFlow** | Alternative/fallback for pure standard-notation rendering if AlphaTab is heavier than needed for the voice/piano side — less guitar-tab-focused. |
| **Tonal.js** | Music theory helpers (scales, intervals, chord names, key signatures) — useful for the random-melody sight-reading generator and for labeling detected chords. |

### Audio capture (shared foundation)

| Library | Use |
|---|---|
| **Web Audio API + AudioWorklet** (browser native) | The audio pipeline: mic → worklet on its own thread → raw PCM buffers fed into the pitch/chord/volume detectors. Everything below consumes this. |

### Voice pitch detection (acapella feature)

| Library | Use |
|---|---|
| **Pitchy** | JS pitch detection using the McLeod Pitch Method; fast and accurate enough for real-time tuner-style use — good fit for note-by-note sight-reading scoring. |
| **@chordbook/tuner** | Web pitch detection for stringed instruments (Web Audio + Pitchy under the hood) with built-in filtering of out-of-range noise and volume-too-low rejection — worth studying even for the voice side, since its noise-filtering approach maps directly onto our "pitch vs. mumbling / background noise" problem. |

### Guitar chord / dynamics detection

| Approach | Use |
|---|---|
| **Custom FFT** on the shared AudioWorklet buffer | No off-the-shelf chord detector exists. Run an FFT (AnalyserNode or worklet), find peak frequencies, match against the fretted note set for the requested chord shape — a fingerprint match rather than a single-pitch problem. |
| **RMS / AnalyserNode volume metering** (native) | Dynamics (loud/soft) and "fuzziness": a clean chord has a tight FFT peak per string; a muted/buzzing string smears energy across frequencies — a reasonable proxy for fuzziness. |

### Computer vision (finger placement, stretch)

| Library | Use |
|---|---|
| **MediaPipe Hand Landmarker** (`@mediapipe/tasks-vision`) | Real-time 21-point 3D hand landmarks from a single camera. (The older `@mediapipe/hands` package is legacy.) We still need our own logic to map landmarks onto fret/string positions — a nontrivial calibration problem; prototype early, treat as stretch. |

### Timing / sync to reference track

| Library | Use |
|---|---|
| **Tone.js** | Wraps Web Audio with a musical clock/transport (BPM-aware scheduling) — useful for "did they strum on the beat" and syncing a backing track/metronome to the lesson. |
| **AlphaTab's alphaSynth** | Already provides tempo-aware playback synced to the notation, so tab-follow-along may not need a separate library. |

### PWA infrastructure

| Tool | Use |
|---|---|
| **vite-plugin-pwa** | Generates the manifest + service worker for installability/offline caching (works with React, Svelte, vanilla). |
| **Workbox** | For manual control over caching strategy (e.g., caching song/notation files for offline practice) beyond the Vite plugin's defaults. |
