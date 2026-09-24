# Tech Stack

## Web PWA 

We're going with **plain-web / JS PWA**, not Flutter.

**Why:** PWA is a single codebase deployed like a normal website — no separate native build pipeline per platform. The one real technical risk (mic access + low-latency AudioWorklet processing on mobile Safari) exists either way, since it's a browser-engine limitation, not a framework choice — so PWA doesn't add any new risk Flutter would have avoided.

> Implementation note: build and test the pitch-detection pipeline **on an actual phone in Safari** before committing further — that's the biggest unknown, regardless of which UI framework sits on top.

## UI framework: React

**Decision: React**, bundled with **Vite** as the build tool.

**Why:** Vite is the tool that packages and optimizes our JS/HTML/CSS into something that runs fast in a browser, and the PWA plugin is built specifically to plug into it. React is the most common pairing with Vite, and lets the UI be built out of small reusable pieces ("components") instead of one large tangled file — this matters here specifically because the UI layer needs to display live feedback from the scoring engine on every note, and component-based UI makes that kind of frequent, targeted screen updates easier to manage than plain hand-written JS.

## Server: Supabase 

The "Server" box in the architecture diagram is **Supabase**, not a custom Node/Express backend. Supabase bundles Postgres (DB), authentication, and file storage behind a JS SDK and auto-generated REST API. For V1, the server only needs to do CRUD (auth, save scores/progress, serve song files) — all of which Supabase covers out of the box. A custom backend would only become necessary if we need server logic Supabase can't express directly.

## Library list (web/JS stack), by feature

### Notation & tab rendering — one renderer per instrument

**Decision (M2):** guitar renders with **alphaTab**, voice renders with
**OpenSheetMusicDisplay (OSMD)**. Both read MusicXML, so the song library stays one
format.

**Why two:** alphaTab is the only option that draws guitar tab, and it plays and
exports what it renders. The voice side was built on OSMD first because its cursor
iterator hands us the timing model (expected notes + playback schedule) for free, and
voice never needs tab.

| Library | Use |
|---|---|
| **alphaTab** (guitar) | Tab + standard notation side by side; loads Guitar Pro 3–8, alphaTex, or MusicXML with `<technical>` string/fret tags. Built-in synth (alphaSynth) for reference playback and cursor; `MidiFileGenerator` exports MIDI and `Gp7Exporter` exports Guitar Pro. It does **not** import MIDI or derive frets from pitch — MIDI → tab goes through our MIDI → MusicXML converter plus a fret-assignment step. |
| **OSMD** (voice) | Standard notation from MusicXML; its cursor iterator is the source of truth for expected notes and playback timing on the voice side. |
| VexFlow | Fallback for pure standard notation (OSMD is built on it). |
| Tonal.js | Music theory helpers (scales, intervals, chord names, key signatures) — useful for the random-melody sight-reading generator and for labeling detected chords. |

### Audio capture (shared foundation)

| Library | Use |
|---|---|
| Web Audio API + AudioWorklet (browser native) | The audio pipeline: mic → worklet on its own thread → raw PCM buffers fed into the pitch/chord/volume detectors. Everything below consumes this. The worklet sees every sample (no polling gaps), so it also detects strum onsets with sample-accurate timestamps — which guitar needs to open its chord-detection window. Supported in Safari 14.5+ on iOS; the mic needs HTTPS and a user tap to start. First consumer: the guitar tuner (F39). |

### Voice pitch detection (acapella feature)

| Library | Use |
|---|---|
| **Pitchy** | JS pitch detection using the McLeod Pitch Method; fast and accurate enough for real-time tuner-style use — good fit for note-by-note sight-reading scoring. |
| `@chordbook/tuner` | Web pitch detection for stringed instruments (Web Audio + Pitchy under the hood) with built-in filtering of out-of-range noise and volume-too-low rejection — worth studying even for the voice side, since its noise-filtering approach maps directly onto our "pitch vs. mumbling / background noise" problem. |

### Guitar chord / dynamics detection

| Approach | Use |
|---|---|
| **Custom FFT** on the shared AudioWorklet buffer | No off-the-shelf chord detector exists. Run an FFT (`AnalyserNode`, browser-native — no library needed), find peak frequencies, match against the fretted note set for the requested chord shape — a fingerprint match rather than a single-pitch problem. |
| RMS / AnalyserNode volume metering (native) | Dynamics (loud/soft) and "fuzziness": a clean chord has a tight FFT peak per string; a muted/buzzing string smears energy across frequencies — a reasonable proxy for fuzziness. |

*Note: raw FFT is intentionally reserved for chords (multiple simultaneous frequencies). Single-note pitch (voice or one guitar string) uses Pitchy instead, because plain FFT peak-picking is noisy on real instrument signals — autocorrelation-based methods handle that better.*

### Computer vision (finger placement, stretch — V2+)

| Library | Use |
|---|---|
| MediaPipe Hand Landmarker (`@mediapipe/tasks-vision`) | Real-time 21-point 3D hand landmarks from a single camera. (The older `@mediapipe/hands` package is legacy.) We still need our own logic to map landmarks onto fret/string positions — a nontrivial calibration problem; prototype early, treat as stretch. |

### Timing / sync to reference track

| Library | Use |
|---|---|
| Tone.js | Wraps Web Audio with a musical clock/transport (BPM-aware scheduling) — useful for "did they strum on the beat" and syncing a backing track/metronome to the lesson. |
| AlphaTab's alphaSynth | Already provides tempo-aware playback synced to the notation, so tab-follow-along may not need a separate library. |

### PWA infrastructure

| Tool | Use |
|---|---|
| vite-plugin-pwa | Generates the manifest + service worker for installability/offline caching (works with React, Svelte, vanilla). |
| Workbox | For manual control over caching strategy (e.g., caching song/notation files for offline practice) beyond the Vite plugin's defaults. |
