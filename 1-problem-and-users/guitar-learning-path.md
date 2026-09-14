# Guitar Learning Path — User Journey, Modes, and Feature Parity

**Owner:** James · **Milestone:** M1 presentation companion
**Scope:** the guitar side only. Voice sight-reading is covered in
[user-stories.md](user-stories.md) and Eduardo's vocal walkthrough.

This document does three things:

1. Walks the path a beginner takes from installing Harmonic to playing their first chord.
2. Defines the guitar **practice modes**, mirroring the structure voice already has.
3. Audits **feature parity** against voice and proposes the requirements that close the gap.

> \*\*The claim this whole path is built on:\*\* every competitor starts by telling a
> beginner to put a finger on the second fret — to someone who has never heard the word
> \*fret\*. Harmonic starts one step earlier.

\---

## The path at a glance

|Stage|What the user does|What the app does|Requires audio?|
|-|-|-|-|
|0|Opens the app, grants mic access|Sound check + level meter|Mic only|
|1|Sees the lesson map|One node unlocked, the rest greyed|No|
|2|**Lesson 1 — Meet the guitar**|Names the parts; a tap-a-part check|**No**|
|3|**Lesson 2 — E minor**|Explains the chord before asking for it|No|
|4|Plays E minor on the practice screen|Listens, verifies, responds|Yes|
|—|Chooses how to practice|Guided / straight-through / changes drill|Yes|
|5|Finishes the run|Hands off to progress review|—|

Stages 1–3 need no working microphone. That is deliberate: **a beginner reaches real
instruction before our hardest technical problem can fail them.**

\---

## Stage 0 — First run and sound check

**What the user sees:** a microphone permission prompt, a live level meter, and one
instruction: *play any string.* No account wall, no instrument survey, no tour.

> \*\*As a beginner who just installed a guitar app,\*\* I want to be playing within a
> minute of opening it, so that setup doesn't become the first place I lose interest.

> \*\*As a user granting microphone access,\*\* I want to immediately see that the app can
> actually hear me, so that I trust the feedback it gives me later.

The level meter is doing quiet work: it is the first and cheapest proof that detection
functions on this user's device, before any score depends on it.

**Open gap — tuning.** None of the current spec documents cover a tuner, and an
out-of-tune guitar makes every downstream detection claim false. Pitch detection gives
us a tuner nearly for free, so this is a gap to close rather than a hard problem. Not
designed yet; flagged here so it isn't discovered late.

\---

## Stage 1 — The lesson map

**What the user sees:** a Duolingo-style path. Node 1 is available. Everything after it
is greyed out.

> \*\*As a beginner,\*\* I want lessons on an unlocking map that rises in difficulty
> gradually, so that I don't jump into complexity that makes me quit.

Covers [F2](../2-scope/requirements.md) (unlocking map, prerequisites) and directly
targets the burnout problem in [problem.md](problem.md): beginners can't skip ahead into
the material that ends the hobby.

\---

## Stage 2 — Lesson 1: Meet the guitar

**This is the lesson that distinguishes the guitar path.** It is not a chord. It is the
instrument.

**What the user sees:** a labeled diagram of a guitar — headstock, tuning pegs, nut,
neck, frets, the six strings with their names low to high (E A D G B E), body, bridge.
Then a quick check that asks them to tap a named part: *"tap the 3rd fret."*

> \*\*As someone who has never held a guitar,\*\* I want the app to name the parts of the
> instrument before it gives me instructions that use those words, so that I'm not
> quietly lost from the first lesson onward.

> \*\*As a beginner,\*\* I want my first lesson to be something I cannot fail for technical
> reasons, so that my first experience of the app is learning rather than troubleshooting.

Three reasons this lesson earns its place:

1. **Every competitor assumes the vocabulary.** Simply Guitar, Yousician and Fender Play
all open with fret- and string-numbered instructions. A learner who doesn't know the
words either guesses or quits, and neither shows up in the app's analytics.
2. **The rest of the product depends on it.** Every label on the practice screen — fret,
string, nut — is unreadable without this lesson.
3. **It needs no microphone.** Lesson 1 is knowledge-only, so it works correctly even
before chord detection is reliable. See [Risks](#risks-and-drawbacks).

**Spec implication:** the lesson map now needs a **knowledge-only node type** alongside
the play-along type. This is a small extension to
[F2 and F3](../2-scope/requirements.md) and is not currently written down anywhere else.

\---

## Stage 3 — Lesson 2: E minor

**What the user sees:** a concept card. What an E minor chord is, a fretboard diagram
with two dots, and why those two notes make it minor. Still no playing.

> \*\*As a beginner trying to learn guitar from an app,\*\* I want short lessons that explain
> the concept first, so that I understand the language instead of memorizing shapes.

This is the [design philosophy](../design-philosophy.md) spine — *theory first, then the
technique that proves it landed* — applied to the concrete first chord.

**Why E minor:** two fingers, all six strings ring, and it is the conventional first
chord in nearly every beginner curriculum. It is also, from
[user-pain-stories.md](user-pain-stories.md), the exact chord a ten-year-old rage-quit
Simply Guitar over when detection failed him.

\---

## Stage 4 — The practice screen

**What the user sees:** a split view.

```
┌───────────────────────────┬────────────────────────────────────┐
│  LEFT — chord diagram     │  RIGHT — notation                  │
│  E minor, two dots        │  tab staff                         │
│  live per-string state    │  standard staff                    │
│  (six indicators)         │  playhead cursor, click to seek    │
├───────────────────────────┴────────────────────────────────────┤
│  FEEDBACK BAR   ✓ E minor — heard it   \[hint] \[skip] \[retry]   │
└─────────────────────────────────────────────────────────────────┘
```

> \*\*As a guitarist,\*\* I want to read tabs with standard notation alongside, because tab
> is what guitarists actually use and I'd like to learn to read while I play. \*(F5)\*

> \*\*As a user practicing a passage,\*\* I want to click or drag anywhere in the music to
> start from that spot, so that I can drill the part I'm actually failing. \*(F7)\*

> \*\*As a beginner,\*\* I want to see which specific string the app is and isn't hearing,
> so that I can fix the actual problem instead of re-strumming and hoping. \*(F16, F17)\*

### What the app is actually checking in V1

**The app already knows which chord it asked for.** So the V1 question is
*verification*, not *recognition*: does the audio match the one expected chord, yes or
no. That is a materially easier problem than identifying an arbitrary chord from sound,
and it is the honest description of what [F16](../2-scope/requirements.md) commits to.

Chord *cleanliness* — naming the muted or under-pressed string — is the ambition
([F17](../2-scope/requirements.md), a "should"), not the V1 guarantee.

\---

## Practice modes

Voice ships two modes: **guided** (F13, must) and **practice** (F14, should, "V2 of the
interface, still this semester"). Guitar mirrors that split, and adds one mode voice has
no reason to want.

|Mode|What it does|Voice equivalent|Ships|
|-|-|-|-|
|**Learn**|One chord at a time, gated, with hint / skip / three-strike|Guided mode (F13)|V1|
|**Play**|Straight through at tempo, nothing stops you, summary at the end|Practice mode (F14)|V1, second|
|**Changes**|Two chords alternating at a set tempo, ungated, scored on clean changes|*none*|V2|

### Learn mode (mirrors voice guided mode)

The lesson holds on the current chord until the app verifies it. The unit of advance is
a **strum of a held shape**, not a sustained pitch: the detection window opens on strum
onset and closes roughly 400 ms into the ring.

**One deliberate difference from voice.** The vocal gate is strict — the cursor does not
advance until the right note is sung. Guitar's gate must be **softer**: after N attempts
it advances anyway and records the result. A strict gate is only as trustworthy as the
detection behind it, and a false negative on a strict gate is precisely the Simply
Guitar failure mode documented in [user-pain-stories.md](user-pain-stories.md) — a
learner stuck for weeks on a level the app wouldn't let them past.

> \*\*As a beginner learning my first chord,\*\* I want the lesson to wait for me rather than
> moving on, so that I get the shape right before anything else is layered on top.
> \*(F28)\*

> \*\*As a beginner whose chord isn't registering,\*\* I want the app to move me forward
> after a few tries instead of holding me there, so that a detection problem doesn't
> become my problem. \*(F28, F29)\*

> \*\*As a user in the middle of a lesson,\*\* I want to skip a chord myself whenever I
> choose, so that I am never dependent on the app's judgment to continue. \*(F30)\*

> \*\*As a beginner who doesn't know a shape,\*\* I want a hint that both plays the chord and
> shows me where the fingers go, so that I can learn it rather than guess at it. \*(F31)\*

### Play mode (mirrors voice practice mode)

The piece runs at tempo, the playhead advances regardless of what is detected, and
nothing gates or stops. Same role the vocal practice mode serves: rehearsing under
performance conditions rather than note by note.

Afterwards the user gets a **played-vs-score** breakdown: for every expected chord,
verified / wrong chord / not heard, plus early / on / late against the beat, rendered as
marks over the tab so they can see *where* in the piece it fell apart.

> \*\*As a more confident player,\*\* I want to play a piece straight through without being
> stopped, so that I can rehearse the way I would actually perform it. \*(F32)\*

> \*\*As a user reviewing a run,\*\* I want to see which chords landed and which were late,
> marked on the music itself, so that I know exactly what to drill next. \*(F33)\*

### Changes mode (V2 — no voice equivalent)

**The skill guitar is teaching isn't in either mirrored mode.** Vocal sight-reading is
note by note, so a note-by-note gate matches the skill. But for a beginner guitarist the
hard part isn't *forming* E minor — it's *getting to* E minor from something else, in
time. Any mode that pauses between chords removes the thing being learned.

Changes mode: two chords alternating at a user-set tempo, ungated, scored on clean
changes per window. This is also the mode where
[F18](../2-scope/requirements.md) (strumming pattern vs. expected) becomes measurable,
since a strum pattern cannot be evaluated one chord at a time.

Deferred to V2 deliberately — it depends on both the gate and the timing score working
first.

\---

## Feature parity with voice

All 23 vocal features, and where guitar stands against each.
**13 have · 2 partial · 8 missing** — and every gap sits in the vocal-specific block.

### Vocal-specific features

|#|Voice|Guitar counterpart|Status|
|-|-|-|-|
|1|Guided gate — won't advance until correct note (F13)|Won't advance until correct chord|**Missing** → F28|
|2|Three misses → auto-skip (F13)|Same, with a silence-timeout miss|**Missing** → F29|
|3|Manual skip (F13)|Same|**Missing** → F30|
|4|Hint plays the note once (F13)|Hint plays *and* shows the chord|**Missing** → F31|
|5|Practice mode, uninterrupted (F14)|Play mode, straight through|**Missing** → F32|
|6|Post-run sung-vs-score (F14)|Post-run played-vs-score|**Missing** → F33|
|7|Live sung note / relative pitch (F12)|Live chord + per-string state|**Partial** → F34|
|8|Solfège toggle (F15)|Label toggle: frets / notes / fingers|**Partial** → F35|
|9|Random generated melodies (F20)|Random chord progressions|**Missing** → F36|
|10|Slow songs first for sight-reading|Explicit tempo control|**Missing** → F37|
|11|Acapella group sessions (F26)|Multi-instrument songs|**Have** — F26 covers it (stretch)|

### Shared listening features guitar already inherits

|#|Feature|Status|
|-|-|-|
|12|Pitch detection, hit / late / missed (F11)|**Have** — chord-level equivalents in F16, F18|
|13|"Couldn't hear you" state (F21)|**Have** — instrument-neutral|
|14|Dynamics detection (F19)|**Have** — instrument-neutral|

### Shared practice-piece features guitar already inherits

|#|Feature|Status|
|-|-|-|
|15|Practice playlist, 3 songs (F4)|**Have**|
|16|Notation rendering — tab + standard (F5)|**Have**|
|17|Reference audio, toggleable (F6)|**Have**|
|18|Click / drag to seek (F7)|**Have**|
|19|Countdown before a run (F8)|**Have**|
|20|MusicXML import (F9) / MIDI transform (F10)|**Have**|
|21|Run-through history with last score (F22)|**Have**|
|22|Attempt recording (F23)|**Have**|
|23|Patchy-area highlighting (F24)|**Have**|

Guitar also carries three features voice has no counterpart for: chord cleanliness
(F17), strumming pattern and timing (F18), and camera finger-placement (F25, stretch).

\---

## Proposed requirements

Formatted to drop straight into the Listening \& scoring table in
[requirements.md](../2-scope/requirements.md). **Not yet merged — proposal only.**

|#|Requirement|Priority|
|-|-|-|
|F28|Guitar guided mode: lesson holds on the current chord until verified; advances after N attempts rather than blocking indefinitely|M|
|F29|Three misses → auto-skip, recorded in score; a miss is a failed strum **or** a silence timeout with no strum onset|M|
|F30|Manual skip / override, always visible during a lesson|M|
|F31|Hint: play the chord once through the reference synth **and** animate the finger positions onto the fretboard diagram|S|
|F32|Guitar play mode: uninterrupted run at tempo, no gating|S|
|F33|Post-run played-vs-score analysis — per chord: verified / wrong / not heard, and early / on / late — marked on the notation|S|
|F34|Live chord state during a run (expected / heard something else / heard nothing). Per-string indicators depend on F17|S|
|F35|Chord-diagram label toggle: fret numbers, note names, or finger numbers|S|
|F36|Random chord-progression generation from unlocked chords, at a chosen tempo|C|
|F37|Tempo control on the practice screen, 50–100% of written tempo, persisted per song|S → recommend **M**|

**Two notes for whoever merges this.**

**F13, F14, F15 and F20 should be reworded, not duplicated.** They read as vocal
mechanics — *"the correct note"*, *"sung-vs-score"*, *"plays the note once"*. If F28–F37
are added beside them unchanged, the table ends up with two parallel near-duplicate sets.
The cleaner edit is to make F13/F14/F15/F20 instrument-neutral and let the guitar IDs
specify instrument-specific behavior underneath. This also supports the modularity
argument in [rough-architecture.md](../3-architecture/rough-architecture.md): one set of
mode rules, different analyzers plugged in.

**F37 is argued up to must.** *"Doesn't even let you choose the tempo"* is a verbatim
competitor complaint in [user-pain-stories.md](user-pain-stories.md), and chord changes
are precisely the skill that requires slowing down. Voice got slow material chosen for
it; guitar needs the user-facing control instead.

\---

## Risks and drawbacks

Ranked. Each is a reason V1 is scoped the way it is, not a reason to abandon the feature.

### 1\. Polyphonic chord detection is the real unsolved problem *(hardest)*

Single-note pitch detection is solved and has libraries we can use. Six strings ringing
at once is not: there is no off-the-shelf chord detector, and the overtones of six
strings overlap in the spectrum. Distinguishing a *muted* string from an *absent* one is
harder still.

**What we do about it.** Constrain the problem. Verify against the one chord we asked
for instead of identifying from all of them. Ship a handful of open chords in V1, not the
fretboard. Keep cleanliness detection out of V1 scope.

### 2\. Wrong feedback is worse than no feedback *(highest user impact)*

From our own research: a reviewer's cough scored as a perfect Fmaj7; users who couldn't
tell whether they played wrong or the app heard wrong. A false positive doesn't merely
annoy — it invalidates every other score the app has given.

**What we do about it.** An explicit "couldn't hear you" state instead of scoring silence
as a miss ([F21](../2-scope/requirements.md)); the soft gate in F28; and detection never
gates progression, so a detection bug costs a point, not the session.

### 3\. Real-time compute on a phone *(most tractable)*

Continuous audio analysis, notation rendering and playback running together means
latency, battery drain and thermal throttling — and mobile Safari is the strictest
environment we would ship into ([N1, N2](../2-scope/requirements.md)).

**What we do about it.** One shared audio buffer feeding the analyzers rather than three
parallel pipelines. Measure on real hardware before building on top of it. Desktop-first
is the fallback if it doesn't hold.

### 4\. Dependency risk

The guitar features sit on the shared audio pipeline. A slip in that module is a slip
here, regardless of how the guitar UI progresses. F34's per-string tier additionally
depends on F17 landing.

\---

## Open questions

1. **Tuning** — is a built-in tuner part of onboarding, or assumed away? Currently
unspecified anywhere in the repo.
2. **Handoff boundary** — confirm with Jamie that this walkthrough ends at live feedback;
run-through summaries (F22–F24) are his.
3. **Lesson 1 depth** — how many parts does the anatomy lesson name? Current proposal
caps it at roughly eight to keep it a five-minute lesson.
4. **Acoustic vs. electric** — the anatomy lesson currently shows one instrument. Does it
need to branch?
5. **Gate threshold** — what is N in F28? Proposal is 3, matching F29's miss count, so a
user never sees two different numbers.
6. **F37 priority** — should tempo control be must or should? This document argues must.
7. **Requirement renumbering** — does the team accept rewording F13/F14/F15/F20 as
instrument-neutral, or prefer parallel guitar-only IDs?

\---

## Adoption plan

This document is a **staging area, not a destination.** A feature with no row in
`requirements.md` doesn't get assigned, estimated, or built — so the content below has to
move out of here to matter.

**Phase 1 — now (this document).** Modes, parity audit, and the F28–F37 proposal live
here so the whole argument is reviewable in one sitting before any shared file changes.

**Phase 2 — next team sync after M1.** Fan out:

|Destination|What moves there|
|-|-|
|[`2-scope/requirements.md`](../2-scope/requirements.md)|F28–F37 rows; reword F13/F14/F15/F20|
|[`2-scope/v1-scope.md`](../2-scope/v1-scope.md)|Learn/Play mode split as In-V1 bullets, mirroring the two voice bullets; tempo control; random progressions into the conditional bullet|
|[`user-stories.md`](user-stories.md)|The mode stories above, into "Beginner guitarist"|
|[`design-philosophy.md`](../design-philosophy.md)|Guitar hint into "Failsafes over frustration"; label toggle beside the solfège line in "Meet players where they are"|
|[`2-scope/potential-problems.md`](../2-scope/potential-problems.md)|Soft-gate rationale; F34's dependency on F17|
|[`3-architecture/tech-stack.md`](../3-architecture/tech-stack.md)|Tempo → Tone.js, progressions → Tonal.js, hint animation → alphaTab (annotating existing rows)|
|[`3-architecture/rough-architecture.md`](../3-architecture/rough-architecture.md)|Guitar gate semantics on the scoring-engine node — **Arsalan's file**|

**Phase 3 — after the fan-out.** Strip the requirement definitions out of this document
and leave a pointer to `requirements.md`. If both files carry full definitions they will
drift, and the narrative is the one that goes stale.

\---

## Slide mapping

|Slide|Covers|
|-|-|
|1 — "The first five minutes"|Stages 0–3|
|2 — "The practice screen"|Stage 4, Learn mode|
|3 — "What could go wrong"|Risks 1–3|

Related: [design-philosophy.md](../design-philosophy.md) ·
[user-stories.md](user-stories.md) · [requirements.md](../2-scope/requirements.md) ·
[potential-problems.md](../2-scope/potential-problems.md)

