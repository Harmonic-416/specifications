# Rough Architecture

(Second pass — Mermaid diagram now included as real source, not just a picture, so it renders directly on GitHub and is easy to edit. See `tech-stack.md` for the resolved Flutter/PWA decision.)

```mermaid
flowchart TB
    subgraph Client["Client (PWA)"]
        subgraph AudioPipeline["Audio pipeline"]
            Mic["Mic (getUserMedia)"]
            Worklet["AudioWorklet<br/>raw PCM on its own thread"]
            Pitch["Pitch detector<br/>(Pitchy — voice + single notes)"]
            Chord["Chord/FFT analyzer<br/>(identity, fuzziness, muted strings)"]
            RMS["RMS metering<br/>(dynamics, 'couldn't hear you')"]

            Mic --> Worklet
            Worklet --> Pitch
            Worklet --> Chord
            Worklet --> RMS
        end

        Playback["Playback / transport<br/>(alphaSynth or Tone.js —<br/>countdown, tempo clock)"]
        Notation["Notation renderer<br/>(alphaTab: tab + standard,<br/>click-to-seek)"]
        Scoring["Scoring engine<br/>hit/late/missed vs.<br/>expected notes,<br/>guided-mode rules (3-miss skip, hints)"]
        UI["UI layer<br/>lesson map · playlist ·<br/>summaries"]

        Playback --> Notation
        Notation -- "expected notes + timing" --> Scoring
        Pitch --> Scoring
        Chord --> Scoring
        RMS --> Scoring
        Scoring -- "live feedback" --> UI
    end

    subgraph Server["Server (Supabase)"]
        API["REST API<br/>(Supabase auto-generated)"]
        Auth["User auth"]
        DB["DB<br/>users · progress · scores"]
        Storage["Storage<br/>songs (MusicXML) ·<br/>attempt recordings"]

        API --> Auth
        API --> DB
        API --> Storage
    end

    UI -.->|"score submission"| API
    Notation -.->|"MusicXML fetch"| Storage

    subgraph Future["Future / stretch (V2+)"]
        HandTrack["MediaPipe hand tracking<br/>finger placement"]
        Group["Group sessions ·<br/>collaborators"]
    end

    Worklet -.-> HandTrack
    API -.-> Group
```

## Key decisions embedded in this sketch

1. **All real-time audio analysis happens on the client.** Streaming mic audio to a server can't meet note-by-note latency, and processing locally avoids the heavy-data problem for the live path. Only *results* (scores) and *optional recordings* (compressed) go to the server.
2. **The notation renderer is the source of truth for "expected notes."** alphaTab parses the score; the scoring engine compares detected vs. expected using the playback transport's clock. One clock, no drift.
3. **The server is thin in V1:** auth, progress, scores, song files — all handled by Supabase directly, no custom backend needed. All the future social features (group sessions, collaborators) hang off the same API later without touching the audio pipeline.
4. **The three analyzers (pitch / chord / volume) share one AudioWorklet buffer** — voice and guitar features are the same pipeline with different analyzers plugged in.

## Instrument-specific detail: voice vs. guitar

Both instruments start from the same shared buffer (decision #4). They diverge at the analyzer stage because the physical signal is different:

| | Voice | Guitar — single note | Guitar — chord |
|---|---|---|---|
| **Signal shape** | One fundamental frequency at a time | One fundamental frequency at a time | Multiple simultaneous frequencies (one per ringing string) |
| **Algorithm** | Pitchy (autocorrelation / McLeod pitch method) | Pitchy (same as voice) | Raw FFT via `AnalyserNode`, peak-picking matched against the expected chord's frequency fingerprint |
| **Why not plain FFT for single notes** | Real signals are noisy; the loudest FFT peak isn't reliably the true pitch. Autocorrelation-based methods are more robust for this. | Same reasoning as voice | N/A — chords need the full spectrum since there's no single dominant peak by definition |
| **Extra signal used** | Volume/clarity threshold (reject too-quiet or unclear input) | Same volume/clarity gate | RMS energy spread — a clean chord has a tight FFT peak per string; a muted/buzzing string smears energy across frequencies, giving a proxy for "fuzziness" |
| **Output to scoring engine** | Normalized `{note, timestamp, confidence}` event | Same shape | Same shape — the scoring engine never knows whether the event came from voice, single-string, or chord detection |

That last row is the important one: every analyzer normalizes its output to the same event shape before it reaches the scoring engine. That's what makes the modularity story (below) actually true rather than just a diagram claim.

## Why this is modular / scales to new instruments

Two separate things make new instruments cheap to add later, and both are already visible in the diagram shape above rather than being a future rewrite:

1. **Pluggable analyzers on a shared pipeline.** Pitch, chord, and volume detectors are three independent modules reading the same AudioWorklet buffer. A new instrument (piano, ukulele, bass) means writing or reusing an analyzer — it does not require touching mic capture, the worklet, or the scoring engine.
2. **An instrument-agnostic scoring engine.** The scoring engine only ever consumes the normalized `{note, timestamp, confidence}` event described above, compared against expected notes parsed from MusicXML/Guitar Pro by alphaTab. It has no instrument-specific logic. So supporting a new instrument is: (a) one new analyzer that emits the standard event shape, plus (b) song data alphaTab already knows how to parse — everything downstream (scoring, UI, storage, progress tracking) is unchanged.

## Open items carried over

- Confirm real-device audio latency on iOS Safari before going further (see `tech-stack.md`, implementation note) — this is the single biggest technical risk regardless of which analyzer or framework is on top.
- MediaPipe hand tracking and group sessions remain explicitly V2+/stretch and are not required for the current milestone.
