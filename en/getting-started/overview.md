---
title: Overview
description: What Cymple is, what the product family contains, and how the data flows from camera to avatar.
tags: [overview, architecture]
updated: 2026-11-10
---

# Overview

## What Cymple is

Cymple is a **DIY-friendly eye and face tracking system for VR**. The hardware is deliberately
simple: one or two ESP32 camera modules per tracker, a printed mount that clips to the headset, and
a USB power source. Everything expensive — computer vision, filtering, expression solving, OSC
routing — happens on the PC inside the **Cymple Console**.

That split is the whole design idea:

- the device only has to capture an image and ship it over Wi-Fi;
- the PC can spend real compute on it (CUDA inference, temporal filters, per-user calibration);
- the protocol is plain OSC, so any app that speaks OSC can consume the output.

## Product family

| Product | What it tracks | Cameras | Where it sits |
|---|---|---|---|
| **Cymple Eye** | Gaze direction, pupil dilation, eyelid openness | 2 (one per eye) | Inside the headset, close to the lenses |
| **CympleFace Dual-Camera Mouth** | Jaw, lips, cheeks, tongue | 2 (stereo pair) | Below the headset, aimed at the lower face |
| **CympleFace Single-Camera Mouth** | Same expression set, lower fidelity | 1 | Below the headset, aimed at the mouth |
| **Cymple Console** | — | — | Windows application, the brain of the system |
| **Cymple VRCFT Module** | — | — | Plugin that lets VRCFaceTracking consume Cymple data |

A full setup (`Eye` + a mouth tracker) drives both eyes and the 28 facial expressions listed in
[Expression Amplitude](../software/expression-amplitude.md). You can run either half alone.

## Data flow

```text
┌──────────────┐   Wi-Fi (JPEG frames)   ┌────────────────────┐
│ ESP32 camera │ ──────────────────────► │                    │
│  left eye    │                         │   Cymple Console   │
└──────────────┘                         │  ┌──────────────┐  │
┌──────────────┐                         │  │ vision +     │  │
│ ESP32 camera │ ──────────────────────► │  │ solver       │  │
│  right eye   │                         │  └──────┬───────┘  │
└──────────────┘                         │         │          │
┌──────────────┐                         │  ┌──────▼───────┐  │
│ mouth camera │ ──────────────────────► │  │ OSC / VRCFT  │  │
└──────────────┘                         │  └──────┬───────┘  │
                                         └─────────┼──────────┘
                                                   │ OSC 9000 / 22999 UDP
                                          ┌────────▼─────────┐
                                          │ VRChat / VRCFT   │
                                          │ avatar           │
                                          └──────────────────┘
```

Two delivery paths exist, and they are mutually exclusive by design:

1. **VRC Direct** — the console talks to VRChat itself over OSC. Nothing else is needed.
2. **External VRCFT** — VRCFaceTracking runs the Cymple module and feeds the avatar through its own
   OSC layer. Useful when you combine Cymple with other trackers, or need VRCFT's unified parameter
   set.

VRC Direct must be off for path 2, because the console only emits compatibility packets while direct
mode is disabled. See [VRCFT](../software/vrcft.md) for details.

## What Cymple is good at

- **Cost.** A DIY eye tracker is a fraction of the price of a commercial unit.
- **Repairability.** Modules are commodity ESP32 boards; a broken camera is a cheap swap.
- **Tinkerability.** Firmware is open, the protocol is documented, the console exposes its filters.
- **Latency.** Local Wi-Fi, no cloud round-trip; the console timestamps and smooths on-device.

## What Cymple is not

- **Not a medical or biometric device.** Gaze accuracy is consumer-grade, in the low single-digit
  degrees at best, and depends heavily on fit.
- **Not plug-and-play.** Expect an evening of printing, flashing and calibrating.
- **Not headset-independent.** The mount must physically fit your headset; the repository ships
  mounts for Quest 2/3/3S/Pro, Pico 4/Neo 3, Pimax Crystal/Dream Air, PSVR2 and a universal clip.
- **Not wireless-free.** The cameras need power; a USB battery or the headset's own port is required.

## Reading order for a new user

1. [Requirements](requirements.md) — check the PC and network first, it saves hours later.
2. [Installation](installation.md) — console, driver, module.
3. [Hardware](../hardware/index.md) — build or buy your tracker.
4. [Network setup](../hardware/network.md) — get the device on Wi-Fi with a fixed IP.
5. [Calibration](../guides/calibration.md) — the step people skip and then complain about.
6. [VRChat setup](../guides/vrchat-setup.md) — avatar parameters and OSC.

---

**Next:** [Requirements](requirements.md) · [Quick start](quick-start.md)

<sub>[Русская версия](../../ru/getting-started/overview.md) · English</sub>
