---
title: Glossary
description: Terms used across the Cymple documentation, in plain language.
tags: [reference, glossary]
updated: 2026-11-10
---

# Glossary

## A–F

**Amplitude** — a gain applied to one expression. `1.00` is neutral; `0` suppresses the shape, `2` doubles it.
See [Expression Amplitude](../software/expression-amplitude.md).

**AP isolation / client isolation** — a router feature that blocks clients from talking to each other.
It breaks every Cymple setup. Must be off.

**Blendshape** — a named deformation of a 3D model. VRChat exposes them as animator parameters; Cymple
drives them over OSC.

**CUDA** — NVIDIA's compute platform. Face inference is much faster with it, hence the GPU advice in
[Requirements](../getting-started/requirements.md).

**Direct mode / VRC Direct** — the console's built-in path to VRChat. On: the console talks to VRChat
itself. Off: it only emits the compatibility stream for an external VRCFaceTracking module.

**FPS / PPS** — frames per second received from a camera / processed samples per second after the
solver accepted them. A large gap between the two points at the image, not the network.

## G–M

**Gaze** — the direction the eye is looking, expressed as a normalised 2D offset. Cymple smooths it
with **Eye Gaze Filter** and scales it with **Eye Gaze Amplitude**.

**INI file** — the plain-text settings store at `%LOCALAPPDATA%\Cymple\iniFile.ini`. See
[Configuration file](config.md).

**MJPEG** — motion JPEG: a stream of independent JPEG frames over HTTP. That is what each camera
serves and what the console pulls.

**Module (VRCFT)** — a DLL that teaches VRCFaceTracking a new data source. Cymple ships one
(`CympleFaceTracking`).

## N–S

**OpenVR driver** — `driver_cymple.dll`, loaded by SteamVR so the runtime knows about the tracker and
can start/stop the console with it.

**OSC** — Open Sound Control: a small UDP message protocol. VRChat speaks it, and so does everything
Cymple talks to.

**Precise Calibration** — a slower, more accurate calibration solve on the [Eye](../software/eye.md) page.

**Priority (module)** — lower number wins a data domain. Cymple is fixed at `0` ("Fixed Highest").

**Pupil dilation** — pupil size change, transmitted in the `0–1` range, scaled by **Pupil Dilation
Amplitude** where `1` keeps the original and `0` holds neutral.

**Recenter** — reset the neutral eye centre and eyelid baselines. One second, done every session.

**ROI** — region of interest: the rectangle the mouth solver treats as the mouth. Can be automatic or
drawn manually.

**Saccade** — a fast jump of the gaze. Why range calibration matters: uncalibrated ranges clip saccades.

## T–Z

**Tracker kit** — pre-built hardware alternative to the DIY build, pre-flashed and mounted.

**VRCFaceTracking (VRCFT)** — the open-source expression-tracking integrator and its parameter standard.
Cymple both emulates and ships a module for it.

**VRChat avatar parameter** — the named value an avatar's animator reads. If the name does not match,
the data is silently dropped.

## Numbers you will see

| Number | Meaning |
|---|---|
| `9000` | VRChat's OSC receive port; Cymple sends here |
| `9001` | VRChat's OSC send port; Cymple listens here |
| `9002` | Cymple's device-input port for third-party OSC relay |
| `22999` | UDP port of the Cymple→VRCFT compatibility packet (70 fields) |
| `4.20.2` | Console version documented in this wiki |

---

**Next:** [Troubleshooting](troubleshooting.md) · [Ports](ports.md)

<sub>[Русская версия](../../ru/reference/glossary.md) · English</sub>
