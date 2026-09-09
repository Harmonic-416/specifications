# Competitors & Examples

## Commercial competitors (and what they prove about the market)

| App | What they do well | Where they fall short | Money / traction |
|---|---|---|---|
| **Yousician** | Real-time pitch detection while you play; gamified songs; guitar/piano/bass/uke/voice | Reviewers: "lacks … rather crucial blackboard information, namely theory and technical explanations" | 20M+ monthly active users across its products (incl. GuitarTuna); raised $28M Series B |
| **Simply Guitar / Simply Piano** (JoyTunes → "Simply") | Extremely polished onboarding; mic-based feedback | No instruction at all for slides, bends, hammer-ons, or pull-offs — songs, not technique | $1B valuation (2021), ~$100M revenue in 2020, $93M+ raised — proof this market pays |
| **JustinGuitar** | Best-in-class graded lesson structure; beloved free content | No listening/feedback loop; video-only | Sustained for years on donations + paid app; huge goodwill moat |
| **StringKick** | Teaches theory/"the language" well | No structured progression or real-time feedback | Content/courses business |
| **Duolingo** (model, not competitor) | The unlocking skill-map progression we're borrowing; proves streaks + short lessons retain beginners | Not music | Public company — the retention model demonstrably pays |
| **Rocksmith+ (Ubisoft)** | Real-audio note detection at scale | Song-first, subscription fatigue, no theory spine | Major-publisher backing shows demand for "listens while you play" |
| **Soundslice** | Best-in-class web notation/tab player synced to audio/video; practice looping | A practice *tool*, not a curriculum | Profitable indie SaaS; licenses its player — "stuff that pays well" without VC |
| **Ultimate Guitar / Songsterr** | Tabs are how guitarists actually read — massive libraries | No teaching, no feedback | Long-running subscription businesses on tabs alone |

**The gap Harmonic targets:** nobody combines StringKick-style theory,
JustinGuitar-style progression, and Yousician-style listening with feedback that's
better than binary correct/incorrect.

## Open-source projects to learn from (or borrow)

| Project | What it is | Why it matters to us |
|---|---|---|
| [PickHero](https://github.com/Artemarius/PickHero) | Free, open-source desktop guitar practice app: real-time pitch detection (YIN algorithm), scrolling tab playback, reads Guitar Pro files — a self-described "lightweight Yousician alternative" | The closest OSS analog to our guitar feature; study its pitch-detection + tab-sync approach |
| [SightreadingPractice](https://github.com/DavidCEllis/SightreadingPractice) | Generates random sheet music, reads MIDI/audio input to check notes; VexFlow display, experimented with the Crepe (TensorFlow) pitch tracker | Directly prefigures our "generated random melody" sight-reading feature |
| [MuseScore](https://github.com/musescore/MuseScore) | The open-source notation editor; huge score ecosystem | Our import target format; its file handling is reference code |
| [alphaTab](https://github.com/CoderLine/alphaTab) | Open-source notation + guitar tab rendering with built-in synth playback | Already our core rendering pick — it's OSS, so we can read the source when stuck |
| [VexFlow](https://github.com/0xfe/vexflow) | Open-source standard-notation renderer | Fallback renderer; used by SightreadingPractice above |
| [OpenSheetMusicDisplay](https://github.com/opensheetmusicdisplay/opensheetmusicdisplay) | Open-source MusicXML renderer built on VexFlow | If MusicXML import becomes central, this is the proven path |
| [TuxGuitar](https://github.com/helge17/tuxguitar) | Long-lived open-source Guitar Pro-style tab editor/player | Reference for tab playback semantics |
| GitHub topics: [music-education](https://github.com/topics/music-education), [pitch-detection](https://github.com/topics/pitch-detection), [sight-reading](https://github.com/topics/sight-reading), [ear-training](https://github.com/topics/ear-training), [chord-detection](https://github.com/topics/chord-detection) | Curated ecosystems | Ongoing mining ground for prior art (e.g., Bemol, an OSS relative-pitch ear trainer) |

## Takeaways

1. **The market pays.** JoyTunes hit unicorn status and ~$100M revenue on *songs
   without theory*; Yousician holds 20M MAU with *binary feedback*. A better product
   thesis has room.
2. **The hard parts have prior art.** Real-time pitch detection (PickHero, Crepe,
   YIN/McLeod), notation rendering (alphaTab, VexFlow, OSMD), and random-melody
   generation (SightreadingPractice) all exist in the open — we integrate and
   differentiate, we don't invent from scratch.
3. **Indie-profitable is a real path.** Soundslice and JustinGuitar show this niche
   sustains businesses without unicorn scale — relevant to our TestFlight/PWA
   distribution question.

Sources: [PickHero](https://github.com/Artemarius/PickHero) ·
[SightreadingPractice](https://github.com/DavidCEllis/SightreadingPractice) ·
[JoyTunes unicorn — NoCamels](https://nocamels.com/2021/06/joytunes-unicorn-music-education-app/) ·
[JoyTunes $1B — Times of Israel](https://www.timesofisrael.com/music-app-maker-joytunes-said-to-be-new-israeli-unicorn-with-google-investment/) ·
[Simply funding — Tracxn](https://tracxn.com/d/companies/simply/__T8RJAYJclzBT1-gnDo9AmQmccws8X8fh5Lm6aVhJ__g) ·
[Yousician — Crunchbase](https://www.crunchbase.com/organization/yousician)
