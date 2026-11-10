---
title: Eye tracker
description: Build, mount and aim the two-camera Cymple Eye tracker.
tags: [hardware, eye-tracking, diy]
updated: 2026-11-10
---

# Eye tracker

The eye tracker is two independent cameras, one per eye. There is no shared board: each camera is
its own Wi-Fi device with its own IP, which is why the console asks for **Left** and **Right** IPs
separately.

## Parts

| Part | Notes |
|---|---|
| 2 × ESP32 camera module | The classic AI-Thinker-style board fits the printed shells |
| 2 × lens | A wider lens helps on headsets with a short eye-to-lens distance |
| Printed shells | `模型/眼追/` — per-headset lens frames |
| Power | USB, 5 V; both cameras can share one cable with a splitter |
| Fasteners | M2×6 self-tapping screws, or 4×1.5 mm magnets for the magnetic variant |

## Build

1. **Print** the two shells for your headset. Print in black; sand the inside so it does not
   reflect.
2. **Flash** both boards with the eye profile before assembly — the USB port is much easier to reach
   on the bench. See [Firmware](firmware.md); the profile in the flasher is **EYE_V3** for current
   boards.
3. **Fit the cameras** into the shells. Do not overtighten: the module's lens holder is plastic and
   cracks easily.
4. **Mount** the shells on the lens frame. They should sit as close to the lens as possible without
   touching it, angled slightly inward toward the eye.
5. **Route** the USB cable along the headset strap, leaving a service loop so the headset can still
   be adjusted.

## Aim

Aim matters more than resolution.

- Point each camera at the **eye**, not at the lens. You want the iris centred at rest, with room for
  the full range of motion.
- Tilt the camera so the eye appears roughly level — a rotated image costs accuracy and makes eyelid
  detection unreliable.
- If the preview shows the eyelid only, the camera is too low; if it shows the eyebrow, too high.

## Connect

1. Power both cameras and wait ~20 s for boot and Wi-Fi association.
2. In [Eye](../software/eye.md), set **Eye Tracker** to `Cymple Eye Tracker`.
3. Enter the left IP and the right IP.
4. Confirm both previews and that the `FPS`/`PPS` counters at the bottom-left of each preview move.

| Reading | Meaning |
|---|---|
| `FPS` ≈ 0, image frozen | Camera reachable but not streaming — check exposure/lens cover |
| `FPS` ≈ 0, "Waiting for image" | Console cannot reach the IP — firewall, subnet or AP isolation |
| `FPS` 25–30 | Healthy |
| `PPS` lower than `FPS` | Frames arriving but the pupil detector is rejecting them — lighting or aim |

## Lighting

Eye tracking needs *contrast*, not brightness.

- Prefer diffuse, even light. A single strong source creates a specular highlight that hides the
  pupil.
- If your headset has IR illuminators, use an IR-pass filter on the lens so the console sees a clean
  pupil.
- Avoid mixing IR and visible light: the pupil response differs and calibration will drift.

## Calibration and recentering

After mounting, always revisit [Eye](../software/eye.md):

1. **Recenter Now** with the headset on and your eyes relaxed forward.
2. **Start Calibration** across the nine dots; enable **Precise Calibration** if you have patience
   for a slower solve.
3. Recenter again whenever the headset shifts on your face. It takes one second and fixes most
   "the gaze is off to the left" reports.

## Maintenance

- Clean the lens with a dry microfibre cloth only.
- Re-seat the camera if the preview drifts out of focus — the lens threads are friction-fit.
- If one eye dies, swap the camera; the shells are identical left to right.

---

**Next:** [Dual-camera mouth tracker](dual-camera-mouth.md) · [Network setup](network.md)

<sub>[Русская версия](../../ru/hardware/eye-tracker.md) · English</sub>
