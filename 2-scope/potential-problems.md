# Potential Problems

## Audio / pitch detection
- How do we differentiate on-pitch singing from mumbling or just making noises?
- Background noise contaminating the mic signal.
- The "couldn't hear you sing" case — input too quiet to score.
- Sound processing is heavy; we may need to develop methods to compress the data.

## Guitar-specific detection
- No off-the-shelf chord detector exists — chord quality ("fuzziness", muted strings,
  not pressing hard enough) requires custom FFT/spectrum analysis, closer to a
  fingerprint match than single-pitch detection. V1 constrains this to *verification*
  (does the audio match the one expected chord), not arbitrary-chord recognition.
- Verify real-time pitch detection works **on an actual phone in Safari** before
  committing further — this is the biggest technical unknown.
- **Wrong feedback is worse than no feedback.** A strict advance-gate is only as
  trustworthy as the detection behind it — hence the guitar **soft gate** (F28:
  advance after 3 attempts, record the result) and the explicit "couldn't hear you"
  state (F21) instead of scoring silence as a miss.
- Per-string live indicators (F34) depend on cleanliness detection (F17, an S) —
  if F17 slips, F34 degrades to whole-chord state.
- **Tuning (resolved by F39):** an out-of-tune guitar makes every detection claim
  false. The tuner rides on the same pitch detector and lives in the onboarding sound
  check, and scored guitar runs prompt for it (without blocking).
- **Low strings and harmonics:** the low E (82 Hz) is close to the detector's floor and
  its second harmonic can read louder than the fundamental — the tuner median-filters
  frames and snaps to the nearest string within ±600¢ so it doesn't jump strings.

## Guitar notation conversion
- alphaTab renders tab only when the file carries string/fret data (Guitar Pro,
  alphaTex, MusicXML with `<technical>` tags); it does not derive frets from pitch
  and cannot import MIDI. MIDI → tab therefore needs our own fret assignment, and
  its fingerings are *playable* but not always the ones a human would pick.
- alphaTab exports MIDI and Guitar Pro but not MusicXML, so a Guitar Pro upload
  can't be stored as MusicXML — the "store MusicXML only" rule needs a guitar
  exception (open question for the team).
- Plain-text ("ASCII") tabs have no rhythm; any import has to guess durations.

## Computer vision (stretch goal)
- Mapping hand landmarks onto fret/string positions is a nontrivial calibration
  problem (camera angle, guitar position). Prototype early; treat as stretch, not
  core MVP.

## Multi-user / sync
- Syncing playback and practice with other people (group sessions).

## Distribution
- iOS distribution: $99/year developer fee for TestFlight; can't go straight through
  the App Store. What's the realistic path to real users during the semester?
