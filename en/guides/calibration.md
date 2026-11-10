---
title: Calibration
description: Recentering, precise calibration and range calibration — what each one solves.
tags: [guide, calibration, eye-tracking]
updated: 2026-11-10
---

# Calibration

Calibration is where good hardware turns into good tracking, and where most "Cymple is inaccurate"
complaints actually live. There are two independent procedures, and they fix different problems.

## The two procedures

| Procedure | Where | What it establishes | How often |
|---|---|---|---|
| **Recentering** | [Eye](../software/eye.md) → **Recenter Both Eyes** | Neutral eye centre and eyelid baselines | Every session, after any fit change |
| **Range calibration** | [Eye](../software/eye.md) → **Eye Range Calibration** | The full motion envelope, so saccades do not clip | Once per mount, after firmware or big parameter changes |
| **Precise Calibration** | Toggle in the same panel | Uses a slower, more accurate solve for both of the above | On, once the mount is final |

## Recentering

> *"Update both eye centers and eyelid baselines, and sync the precise calibration center."*

Press **Recenter Now** while:

1. the headset is on your head, adjusted as you normally wear it,
2. you are looking straight ahead at a distant point,
3. your face is relaxed — no squint, no raised brows,
4. the previews show live images.

Recenter whenever the gaze drifts, after the headset moves, and after changing
**Eye Gaze Amplitude**. It takes about a second.

> If recentering fixes the problem every time, the mount is moving. Tighten it — no amount of
> software calibration compensates for a camera that slides.

## Range calibration

**Start Calibration** walks you through nine targets. The console records the extremes of eye motion,
which is what keeps fast saccades from saturating at the screen edges.

Prerequisites:

- At least one eye device streaming. Otherwise the panel says *"No eye-tracking device was detected.
  Connect at least one eye-tracking device before starting range calibration."*
- If the button stays disabled with a live preview, run the console as administrator — the panel
  itself suggests this.

Procedure:

1. Fix your head position; do not lean in.
2. Move **only your eyes** to each target.
3. Hold the target until it advances.
4. If you lost a target, restart the calibration rather than continuing.
5. Recenter once at the end.

Expected duration: under a minute with **Precise Calibration** off, two to three minutes with it on.

## When calibration still does not help

Work through this list before assuming a hardware fault:

| Symptom | First suspect | Fix |
|---|---|---|
| Gaze consistently offset in one direction | Mount shifted | Recenter; if it returns, tighten the mount |
| Gaze offset differs between eyes | One camera aimed badly | Re-aim that camera; check its preview |
| Gaze correct at centre, wrong at edges | Range calibration incomplete | Redo range calibration |
| Gaze saturates before the screen edge | **Eye Gaze Amplitude** too high | Lower toward `0.7` |
| Blinks not detected | Eyelid baseline stale | Recenter; raise **Blink Close Amplitude** |
| Eyes look "crossed" in the avatar | **Binocular Gaze Sync Rate** | Raise it slightly |
| Tracking fine, then drifts after 20 min | Headset slipping / heat | Re-seat, recenter |

## Mouth calibration

The mouth pages have no explicit calibration button; the equivalents are:

| Control | Page | Effect |
|---|---|---|
| **Camera Range** | [Dual-Camera Mouth](../software/dual-camera-mouth.md) | Frames the face; the closest thing to calibrating scale |
| **Camera Horizontal Offset** | [Dual-Camera Mouth](../software/dual-camera-mouth.md) | Aligns the stitch |
| **Camera Rotation** | [Single-Camera Mouth](../software/single-camera-mouth.md) | Levels a tilted image |
| **Draw ROI Manually** | [Single-Camera Mouth](../software/single-camera-mouth.md) | Pins the region of interest |
| **Expression Amplitude** | [Expression Amplitude](../software/expression-amplitude.md) | Per-shape gain, the real "calibration" for expressions |

The nearest analogue to recentering for the face is simply re-checking that the neutral face reads as
neutral: open VRChat, relax, and confirm no expression slider sits above zero.

## A calibration ritual that takes 90 seconds

Do this at the start of every session:

1. Headset on, straps adjusted, tracker powered.
2. Previews live, `FPS` healthy.
3. **Recenter Now**.
4. Open VRChat, look at your mirror avatar, blink twice, smile once.
5. If the blink is incomplete or the gaze drifts, recenter again — once.

That is it. Range calibration is a one-time investment per mount, not a per-session task.

---

**Next:** [Dataset recording](dataset-recording.md) · [Eye page](../software/eye.md)

<sub>[Русская версия](../../ru/guides/calibration.md) · English</sub>
