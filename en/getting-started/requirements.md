---
title: Requirements
description: PC, GPU, headset, network and driver requirements for Cymple Console and trackers.
tags: [requirements, setup]
updated: 2026-11-10
---

# Requirements

## PC

| Item | Minimum | Recommended | Why |
|---|---|---|---|
| OS | Windows 10 64-bit (1909+) | Windows 11 64-bit | The console, the OpenVR driver and the flasher are Windows-only |
| CPU | 4 cores / 8 threads | 6 cores or better | One decode + inference thread per camera |
| RAM | 8 GB | 16 GB | VRChat is the real memory consumer |
| GPU | DirectX 11 class GPU | NVIDIA GTX 1650 SUPER or better (CUDA) | Face inference runs far faster on CUDA; the console exposes the device in [Face Settings](../software/face-settings.md) |
| Free disk | 2 GB | 10 GB | Console, logs, optional dataset recordings |
| USB | 1 free port | 2 | Flashing, and powering the tracker while you test |

The console happily runs on integrated graphics, but expect a lower frame rate and a higher CPU
load; the face solver falls back to the CPU. The reference machine in our screenshots uses an
**NVIDIA GeForce GTX 1650 SUPER**, which is a realistic baseline.

## Headset

- Any SteamVR headset works for the *driver* side. The mount is the only headset-specific part.
- Provided mounts: Quest 2, Quest 3, Quest 3S, Quest Pro, Pico 4/4 Pro/4U, Pico Neo 3, Pimax
  Crystal, Pimax Dream Air/SE, PSVR2, plus a universal adhesive clip.
- Standalone Quest tracking does **not** work over Link/Air Link alone — the console needs the
  headset to be running SteamVR on the PC.

## Network

| Requirement | Detail |
|---|---|
| Bandwidth | 2.4 GHz is enough for a single eye camera, 5 GHz strongly recommended for stereo mouth |
| Subnet | The PC and all trackers must be on the **same L2 network** |
| Addressing | Fixed IP per device (either a DHCP reservation or a static IP configured in the device) |
| Isolation | Guest Wi-Fi / AP isolation / "client isolation" must be **off** |
| Firewall | Allow the console through Windows Defender Firewall on private networks |

Each camera is a small HTTP/MJPEG server. The console pulls frames from the IP you type into
[Eye](../software/eye.md) → **Left/Right Eye Device Information** or the mouth pages' **Device Info**.

> **Tip.** If your router has a "gaming" or "IoT" SSID, make sure it is not isolated from the main
> one. AP isolation is the single most common cause of "Waiting for image".

## Software

| Component | Needed for | Where |
|---|---|---|
| Cymple Console | Everything | Distributed as a signed installer / portable ZIP |
| OpenVR driver (`driver_cymple.dll`) | SteamVR to see the tracker as an HMD accessory | Ships in `openvr驱动/cymple/` in the repository |
| VRCFaceTracking | Only if you choose the external-VRCFT path | [vrcft.io](https://vrcft.io) |
| Cymple VRCFT module | Only for the external path | [CympleFaceTracking releases](https://github.com/Dominocs/CympleFaceTracking) |
| VRChat with OSC enabled | Avatar output | In-game: **Options → OSC → Enabled** |
| USB-serial driver (CH340 / CP210x) | [Firmware Flash](../software/firmware-flash.md) | Vendor driver, usually installed automatically |

## Permissions

- **Administrator rights** are needed for two operations only: installing the OpenVR driver into
  `SteamVR/drivers`, and flashing firmware over a COM port.
- If the eye-range calibration is blocked, the console's own hint applies: *"If you encounter any
  issues, run this application as administrator."*

## What you do **not** need

- A dedicated tracker dongle for the DIY build — it is Wi-Fi only.
- A Meta account, cloud login, or any per-seat licence for the console.
- Base stations. Cymple does not add tracking volume; it adds gaze and expression data on top of the
  headset's own 6DoF.

---

**Next:** [Installation](installation.md) · [Quick start](quick-start.md)

<sub>[Русская версия](../../ru/getting-started/requirements.md) · English</sub>
