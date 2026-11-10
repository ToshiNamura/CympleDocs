---
title: Cymple Wiki
description: Product documentation for Cymple eye tracking, face tracking and the Cymple Console.
tags: [home]
updated: 2026-11-10
---

# Cymple Wiki

**Cymple** is a low-cost, open-source eye-tracking and face-tracking system for VR. A pair of small
ESP32 camera modules streams over Wi-Fi to the **Cymple Console**, which turns the raw images into
gaze and 28 facial expressions and delivers them to VRChat — either directly (VRC Direct + OSC) or
through VRCFaceTracking.

This wiki covers three things:

1. **Hardware** — what to build, how to print it, how to put it on the network.
2. **Software** — every page of the Cymple Console, control by control.
3. **Integration** — getting the data into VRChat and into your avatar.

> ⚠️ **Translation notice.** The [Russian version](../ru/index.md) was translated by the AI model
> **DeepSeek-V4.1--Flash** and may contain inaccuracies. These English pages are the source of truth.

## Start here

| If you want to… | Read |
|---|---|
| Understand what Cymple can and cannot do | [Overview](getting-started/overview.md) |
| Check PC, headset and network requirements | [Requirements](getting-started/requirements.md) |
| Install the console, driver and module | [Installation](getting-started/installation.md) |
| Get tracking working in 15 minutes | [Quick start](getting-started/quick-start.md) |
| Build the eye tracker | [Eye tracker](hardware/eye-tracker.md) |
| Build a mouth tracker | [Dual-camera mouth](hardware/dual-camera-mouth.md) · [Single-camera mouth](hardware/single-camera-mouth.md) |
| Configure the device Wi-Fi and IP | [Network setup](hardware/network.md) |
| Flash firmware | [Firmware](hardware/firmware.md) |

## Console reference

The application is organised as a flat sidebar: **Home**, then the **Cympleface** group, then
**Logs**, **Global Settings** and **Feedback**.

| Page | Purpose |
|---|---|
| [Home](software/home.md) | Module switches: Eye Tracking, Face Tracking, VRCFT |
| [Eye](software/eye.md) | Camera previews, IPs, calibration, filters, pupil/gaze amplitudes |
| [Dual-Camera Mouth](software/dual-camera-mouth.md) | Stereo mouth tracking, stitching, camera range |
| [Single-Camera Mouth](software/single-camera-mouth.md) | Monocular mouth tracking with manual ROI |
| [Expression Amplitude](software/expression-amplitude.md) | Per-blendshape gain, 28 sliders |
| [VRCFT](software/vrcft.md) | VRC Direct, port pairing, plugin manager, priorities |
| [Face Settings](software/face-settings.md) | Inference device, reset-on-disconnect |
| [Firmware Flash](software/firmware-flash.md) | Profile choice, serial port, flashing log |
| [OSC Router](software/osc-router.md) | Forward OSC to phones, trackers and extra apps |
| [Logs](software/logs.md) | Runtime log viewer |
| [Global Settings](software/global-settings.md) | Language, theme, SteamVR lifecycle |
| [Feedback](software/feedback.md) | Bug reports and suggestions |

## Guides

- [Calibration](guides/calibration.md) — precise calibration, recentering, range calibration.
- [Dataset recording](guides/dataset-recording.md) — capture your own training data.
- [VRChat setup](guides/vrchat-setup.md) — OSC, avatar parameters, VRCFT outside the console.
- [External VRCFT](guides/external-vrcft.md) — run the module in VRCFaceTracking instead of VRC Direct.

## Reference

- [Ports and endpoints](reference/ports.md)
- [Configuration file](reference/config.md)
- [Troubleshooting](reference/troubleshooting.md)
- [FAQ](reference/faq.md)
- [Glossary](reference/glossary.md)

## Version note

Screenshots in this wiki were captured from **Cymple Console 4.20.2**. Labels and defaults move
between releases; if a control is missing on your build, check [Logs](software/logs.md) for the
version banner and compare with the release notes.

---

<sub>English · [Русская версия](../ru/index.md)</sub>
