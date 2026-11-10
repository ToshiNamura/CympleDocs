---
title: Hardware
description: The Cymple device family, what is in the box, and how to mount it on your headset.
tags: [hardware, devices]
updated: 2026-11-10
---

# Hardware

Every Cymple device is the same idea in a different shape: one or two ESP32 camera modules in a
printed shell, streaming JPEG frames over Wi-Fi, powered from USB.

## Device map

| Device | Cameras | Mounts in the kit | Typical use |
|---|---|---|---|
| **Cymple Eye** (DIY) | 2 × ESP32-CAM | Quest 2/3/3S lens frame, Pico 4 frame | Gaze, blinks, pupil dilation |
| **CympleFace Dual-Camera Mouth** | 2 × ESP32 camera | Under-headset arm | Full 28-expression set with depth |
| **CympleFace Single-Camera Mouth** | 1 × ESP32 camera | Under-headset clip | Same set, cheaper, no stereo depth |
| **USB dongle / tracker kit** | — | Pre-built kits only | Pre-flashed alternative to the DIY route |

The repository ships the printable parts under `模型/`, split into `支架_最新` (current mounts),
`眼追` (eye tracker shells), `面捕` (mouth tracker shells) and `cympleface_3dfiles` (editable STEP
sources). Mounts are grouped per headset: Quest 2, Quest 3, Quest 3S, Quest Pro, Pico 4/4 Pro/4U,
Pico Neo 3, Pimax Crystal, Pimax Dream Air/SE, PSVR2 and a universal adhesive clip.

## What you need regardless of variant

- **A Windows PC** that will run the console — see [Requirements](../getting-started/requirements.md).
- **5 GHz Wi-Fi** on the same subnet as the PC, with client isolation disabled.
- **USB power.** A small power bank strapped to the headset strap works; so does the headset's own
  USB port if it supplies enough current.
- **Fasteners.** Most current mounts use M2×6 self-tapping screws; the Pimax and universal mounts use
  nano tape instead.
- **A dark, matte interior.** Light leaks around the lenses are the number one cause of bad eye
  tracking. Print in black, and seal the eye cups.

## Choosing a variant

| You want… | Choose |
|---|---|
| Gaze + blinks only | **Cymple Eye** |
| Full face for VRChat, best quality | **Dual-Camera Mouth** + Eye |
| Full face, tight budget | **Single-Camera Mouth** + Eye |
| No soldering, no flashing | Pre-built tracker kit |
| A phone as the camera | Not supported — the console expects an ESP32 MJPEG endpoint |

## Pages in this section

- [Eye tracker](eye-tracker.md) — build, mount, aim.
- [Dual-camera mouth tracker](dual-camera-mouth.md) — stereo pair, stitching, offsets.
- [Single-camera mouth tracker](single-camera-mouth.md) — monocular build and ROI.
- [Network setup](network.md) — SSID, IP addressing, firewall.
- [Firmware](firmware.md) — profiles, flashing, recovery.
- [Third-party bridges](bridges.md) — feeding Cymple from other trackers.

## Health and comfort

- The camera modules emit a faint IR/visible glow depending on the lens filter. If you see a red
  dot in your peripheral vision, add an IR-pass filter or move the module further from the lens.
- Keep the tracker under ~80 g; heavier assemblies shift the headset's centre of mass and cause
  neck fatigue in long sessions.
- Do not cover the headset's proximity sensor — many headsets will sleep mid-session.

---

**Next:** [Eye tracker](eye-tracker.md) · [Network setup](network.md)

<sub>[Русская версия](../../ru/hardware/index.md) · English</sub>
