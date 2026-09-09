# Potential Problems

## Audio / pitch detection
- How do we differentiate on-pitch singing from mumbling or just making noises?
- Background noise contaminating the mic signal.
- The "couldn't hear you sing" case — input too quiet to score.
- Sound processing is heavy; we may need to develop methods to compress the data.

## Guitar-specific detection
- No off-the-shelf chord detector exists — chord quality ("fuzziness", muted strings,
  not pressing hard enough) requires custom FFT/spectrum analysis, closer to a
  fingerprint match than single-pitch detection.
- Verify real-time pitch detection works **on an actual phone in Safari** before
  committing further — this is the biggest technical unknown.

## Computer vision (stretch goal)
- Mapping hand landmarks onto fret/string positions is a nontrivial calibration
  problem (camera angle, guitar position). Prototype early; treat as stretch, not
  core MVP.

## Multi-user / sync
- Syncing playback and practice with other people (group sessions).

## Distribution
- iOS distribution: $99/year developer fee for TestFlight; can't go straight through
  the App Store. What's the realistic path to real users during the semester?
