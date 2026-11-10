---
title: Dataset recording
description: Capture labelled eye and mouth frames to evaluate or improve tracking.
tags: [guide, dataset, training]
updated: 2026-11-10
---

# Dataset recording

Every tracking page has a **Record Dataset** panel, collapsed by default. It captures the raw frames
the console receives together with the solver's output, so you can review a session offline, compare
builds, or feed a custom training run.

## Where it lives

| Page | Panel subtitle | Content |
|---|---|---|
| [Eye](../software/eye.md) | *"Expand to enter eye-tracking dataset recording."* | Left and right eye frames |
| [Dual-Camera Mouth](../software/dual-camera-mouth.md) | *"Expand to enter stereo mouth-tracking dataset recording."* | Stereo pair |
| [Single-Camera Mouth](../software/single-camera-mouth.md) | *"Expand to enter mouth-tracking dataset recording."* | Single frame |

## Why record

| Goal | Dataset helps |
|---|---|
| Diagnose "why does my mouth look wrong" | You can see exactly what the camera saw versus what the solver produced |
| Compare firmware versions | Same face, same lighting, two builds |
| Compare filter settings | Objective before/after instead of memory |
| Contribute to the project | Labelled data is the scarcest resource in a DIY tracker |
| Train a personal model | Your face, your headset, your lighting |

## Planning a session

1. **Pick one variable.** One lighting condition, one headset fit, one set of filter values.
2. **Record a script.** Read a fixed list of expressions aloud: neutral, smile, frown, wide jaw,
   pucker, blink slow, blink fast, look left, look right, tongue out.
3. **Keep neutral frames.** A few seconds of resting face anchor any later analysis.
4. **Repeat twice.** Two takes per condition tells you whether a difference is real.
5. **Note the metadata** in a text file next to the recording: version, profile, PC, GPU, lighting,
   filter values.

## Storage

Raw camera frames are large. Budget roughly:

| Content | Per minute (order of magnitude) |
|---|---|
| Eye pair, 640×480 | tens of MB |
| Stereo mouth, 640×480 × 2 | tens to ~100 MB |
| With solver output alongside | roughly double |

Recordings land under the console's local app data directory. Check free space before a long session,
and move finished sets to another drive.

## Privacy

A recording contains images of your face and your eyes. Treat it as personal data:

- do not publish a raw set without consent from everyone who appears in it,
- blur or crop before sharing screenshots in a bug report,
- prefer short clips over long sessions when reporting an issue,
- remember that the config INI travels with bug reports too — see [Feedback](../software/feedback.md).

## What a good recording looks like

| Property | Good | Bad |
|---|---|---|
| Lighting | Even, diffuse | Backlit, single hot spot |
| Framing | Face fills the frame, nose visible | Mouth at the very edge |
| Motion | Deliberate, one expression at a time | Constant fidgeting |
| Duration | 30–60 s per take | 20-minute wandering session |
| Labelling | Written script, timestamps noted | "I just moved my face around" |

## After recording

1. Review the frames — the point of the exercise is to *see* the failure.
2. Note the frame range where the tracking broke, in seconds.
3. Reproduce with one setting changed, and re-record.
4. Keep only the pairs that document a real difference; delete the rest.

---

**Next:** [VRChat setup](vrchat-setup.md) · [Eye](../software/eye.md)

<sub>[Русская версия](../../ru/guides/dataset-recording.md) · English</sub>
