# Rough Architecture Sketch

*(First pass — done with Mermaid, per our plan. Assumes the web/PWA direction; see
[tech-stack.md](tech-stack.md) for the open Flutter question.)*

```mermaid
flowchart TB
    subgraph Client["Client (PWA)"]
        UI["UI layer<br/>lesson map · playlist · summaries"]
        Notation["Notation renderer<br/>(alphaTab: tab + standard, click-to-seek)"]
        Playback["Playback / transport<br/>(alphaSynth or Tone.js — countdown, tempo clock)"]

        subgraph AudioPipe["Audio pipeline"]
            Mic["Mic (getUserMedia)"]
            Worklet["AudioWorklet<br/>raw PCM on its own thread"]
            Pitch["Pitch detector<br/>(Pitchy — voice notes)"]
            Chord["Chord/FFT analyzer<br/>(identity, fuzziness, muted strings)"]
            Volume["RMS metering<br/>(dynamics, 'couldn't hear you')"]
        end

        Scoring["Scoring engine<br/>hit / late / missed vs. expected notes<br/>guided-mode rules (3-miss skip, hints)"]
    end

    subgraph Server["Server"]
        Auth["User auth"]
        API["REST API"]
        DB[("DB<br/>users · progress · scores")]
        Files[("Storage<br/>songs (MusicXML) · attempt recordings")]
    end

    subgraph Future["Future / stretch (V2+)"]
        CV["MediaPipe hand tracking<br/>finger placement"]
        Groups["Group sessions · collaborators"]
    end

    Mic --> Worklet
    Worklet --> Pitch & Chord & Volume
    Pitch & Chord & Volume --> Scoring
    Notation -- "expected notes + timing" --> Scoring
    Scoring -- "live feedback" --> UI
    Playback --> Notation
    UI --> API
    API --> Auth & DB & Files
    Files -- "MusicXML" --> Notation
    CV -.-> Scoring
    Groups -.-> API
```

## Key decisions embedded in this sketch

1. **All real-time audio analysis happens on the client.** Streaming mic audio to a
   server can't meet note-by-note latency, and processing locally avoids the
   heavy-data problem for the live path. Only *results* (scores) and *optional
   recordings* (compressed) go to the server.
2. **The notation renderer is the source of truth for "expected notes."** alphaTab
   parses the score; the scoring engine compares detected vs. expected using the
   playback transport's clock. One clock, no drift.
3. **The server is thin in V1:** auth, progress, scores, song files. All the future
   social features (group sessions, collaborators) hang off the same API later
   without touching the audio pipeline.
4. **The three analyzers (pitch / chord / volume) share one AudioWorklet buffer** —
   voice and guitar features are the same pipeline with different analyzers plugged
   in.

## Open questions

- Flutter vs. PWA (changes the client boxes, not the shape) — see
  [tech-stack.md](tech-stack.md).
- Server stack unchosen (Node/Express? Python? Firebase-style BaaS?).
- Where recordings live and how much we compress (ties to N3 in
  [requirements](../2-scope/requirements.md)).
