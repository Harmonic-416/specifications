# Problem & Users

## The problem

Harmonic is a learning app for music. Many beginners drop their instrument because it
gets too complex too fast — they try to learn too quickly and burn out.

**Beginners quit before they understand anything.** Three reasons why the current
market fails them:

1. **Apps teach songs, not the language.** Reviewers found Yousician "lacks a lot of
   what I would consider rather crucial blackboard information, namely theory and
   technical explanations." Simply Guitar has no instruction at all for slides, bends,
   hammer-ons, or pull-offs.
2. **The feedback is binary.** Every app in the category reduces your playing to
   correct or incorrect. None can tell a muted string from a wrong fret from a note
   played slightly late.
3. **Nobody has combined the pieces.** StringKick teaches theory well. JustinGuitar
   structures graded lessons well. No one has put both under a progression that keeps
   a beginner coming back.

(See [competitors-and-examples.md](competitors-and-examples.md) for the full market
breakdown.)

## Users

- **Beginner guitarists** who have tried the market leaders and hated them.
- **Singers / acapella groups** who want sight-reading (solfège) practice with real
  pitch feedback.
- **(Future) piano learners** — the proposal deck scopes Harmonic to
  *Guitar · Voice · Piano*.

See [user-stories.md](user-stories.md) for concrete stories.

## Why does this take a semester?

- Sound processing is very heavy; we will need to develop methods to compress the data.
- Learning paths build to complex topics and require incremental steps to reach.
- **Version 1** will be basic lessons and audio processing. Future versions build on
  these basics: teaching sheet music, more advanced guitar techniques, playthroughs of
  songs, and group interactions between users.
- **Stretch goal:** incorporate video processing to determine finger placement and
  technique, and provide feedback to the user.

## How do we get users?

Open questions:
- Pay the $99 Apple developer fee and distribute via TestFlight?
- Can't go straight through the App Store — what's the path?
- A web PWA would sidestep app-store gatekeeping entirely (see the
  [tech stack](../3-architecture/tech-stack.md) decision).
