---
title: External VRCFT
description: Run the Cymple module inside VRCFaceTracking instead of using VRC Direct.
tags: [guide, vrcft, module]
updated: 2026-11-10
---

# External VRCFT

Sometimes the console should not be the last hop. If you mix trackers, want VRCFaceTracking's unified
parameter set, or need its avatar tooling, run the Cymple module *inside* VRCFT and let VRCFT own the
VRChat connection.

## When to choose this

| Situation | Path |
|---|---|
| Cymple only, simple avatar | [VRC Direct](../software/vrcft.md) — fewer moving parts |
| Cymple + another tracker | External VRCFT — one integrator for both |
| Avatar already rigged for VRCFT | External VRCFT — no rework |
| Debugging a module-level issue | External VRCFT — VRCFT's own logs help |

## Prerequisites

- VRCFaceTracking installed ([vrcft.io](https://vrcft.io)).
- `CympleFaceTracking` release ZIP (DLL + module metadata). VRCFaceTracking supplies the Core runtime.
- The console running with **VRC Direct off**.

## Install the module

1. Open VRCFaceTracking → **Module Manager**.
2. Choose **Install from file** (custom module installer).
3. Select the release ZIP.
4. Restart VRCFaceTracking.
5. Confirm the module is listed and enabled.

## Configure the console

1. [VRCFT](../software/vrcft.md) → turn **VRC Direct** *off*.
2. Leave the ports at `9001` / `127.0.0.1` / `9000` unless VRChat was customised.
3. Watch **Input Rate** — it should stay alive because VRCFT keeps exchanging data with VRChat.

Why direct mode must be off: the console only emits the compatibility packet stream (a 70-field UDP
packet on port `22999`) while direct mode is disabled. With direct mode on, the module has nothing to
read and reports no data.

## Behaviour details

| Aspect | Behaviour |
|---|---|
| Eye and mouth availability | Comes from VRCFT's `Initialize(eyeAvailable, expressionAvailable)` arguments, not from the console's hardware switches |
| Console hardware toggles | `cymple_eye_sw` / `cymple_mouth_sw` cannot disable *another* application's input — the module ignores them by design |
| Domain changes | Applied when VRCFT reinitialises the module |
| Packet flags | Indicate which domains actually carry data |
| Disconnect behaviour | After ~1 s without data, output follows `[Cymple_Mouth] reset_expression_on_tracking_disconnect` (default: reset; `false`: hold the last frame) |
| Where that preference is read | `%LOCALAPPDATA%\Cymple\iniFile.ini`, with the legacy `C:\Cymple\iniFile.ini` fallback; refreshed once per second |
| Gaze and expressions | Pass through Cymple's processed values; the eye deadzone is applied in the console |
| Pupil dilation | Transmitted in the `0–1` range |

### Known limitation

The current Cymple sender can keep transmitting the last mouth sample after the mouth device
disconnects. The packet format has no mouth-device freshness indicator, so the module can detect a
stopped stream but cannot infer a device disconnect from repeated identical samples. If your mouth
freezes rather than resets, this is why — enable **Reset expression after disconnect** and fix the
underlying device link.

## Verification

1. VRCFT shows the Cymple module loaded and enabled.
2. VRCFT's own parameter view shows eye and expression values moving.
3. The console shows a non-zero **Output Rate**? It will *not* — direct mode is off, so the console is
   only emitting the compatibility stream. Judge from VRCFT's side instead.
4. VRChat avatar reacts.

## Reverting

Turn **VRC Direct** back on and disable the external module. Only one path should be active; running
both produces duplicated and conflicting parameter writes.

---

**Next:** [Ports and endpoints](../reference/ports.md) · [VRCFT page](../software/vrcft.md)

<sub>[Русская версия](../../ru/guides/external-vrcft.md) · English</sub>
