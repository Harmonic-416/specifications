# Design Philosophy

**Teach the language, not just the songs.** A user who finishes Harmonic can look at
notation they have never seen and work out how to play it.

## Theory as the spine

Every lesson explains the concept first — what a minor third is, why the fifth string
sits where it does — then asks for the technique that proves it landed.

## Feedback while you play

The app listens through the microphone and scores each note against what the lesson
expected: hit, late, or missed. Feedback goes beyond binary correct/incorrect — the
long-term goal is distinguishing a muted string from a wrong fret from a note played
slightly late.

**See what works: visual or audible feedback** — we should experiment with both.

## A path that grows with you

Short lessons on a Duolingo-style map. Later nodes unlock as earlier ones are cleared,
so difficulty rises without the user having to choose it. This directly targets the
burnout problem: beginners can't skip ahead into complexity that makes them quit.

## Failsafes over frustration

Never let a user get permanently stuck:
- If a note is wrong 3 times, auto-skip it and record that in the overall score.
- Offer a manual skip/override.
- Offer a "hint" — play the note for them once if they don't know what to sing.

## Meet players where they are

- Guitarists read **tabs**, not sheet music — render tab (alongside standard notation
  so reading is learned while playing).
- Solfège display is a **toggle** — not everyone uses it, but it helps with
  relational pitch.
- Slow songs first for sight-reading practice.
