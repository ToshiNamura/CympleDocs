---
title: Troubleshooting
description: Symptom-driven fixes for Cymple hardware, console and VRChat problems.
tags: [reference, troubleshooting]
updated: 2026-11-10
---

# Troubleshooting

Find your symptom, then work the list top to bottom. Entries are ordered by how often they turn out to
be the cause.

## The device

### "Waiting for image" on every preview

1. Is the camera powered? Check for a light on the board.
2. Is it on the same subnet as the PC? `Test-Connection <ip>`.
3. Does `http://<ip>/` answer in a browser?
4. Is AP/client isolation enabled on the router? It must be off.
5. Is the console allowed through Windows Firewall on the *private* profile?

### Preview frozen, `FPS: 0-0`

- Camera reachable but not streaming: power-cycle it.
- Stream server crashed: reflash the firmware.
- Two devices with the same IP: fix addressing.

### `FPS` healthy, `PPS` near zero

The frames arrive but the solver rejects them.

- Aim: is the eye/mouth actually in frame?
- Focus: is the image sharp?
- Lighting: is there contrast, or a blown-out highlight?
- Profile: is the flashed profile correct for this board?

### Device disappears after a few minutes

- Wi-Fi roaming or band steering kicked it off — pin it to one AP/band.
- Power: a weak battery bank sags under load. Try a powered USB port.
- Thermal: an enclosed ESP32 in a hot headset can throttle. Vent the shell.

## The console

### Console will not start / closes at once

- Run it as administrator once, to rule out a permissions problem.
- Check `%LOCALAPPDATA%\Cymple\logs\` for a crash-time file.
- Antivirus quarantine of the OpenVR DLL is a real cause; check its quarantine list.

### Calibration button is greyed out

- No device detected. Fix the preview first.
- If a preview is live and the button is still disabled, run the console as administrator — the panel
  suggests this itself.

### Settings do not stick

- The console was still running when the INI was edited by hand: exit before editing.
- The INI is read-only or owned by another user.
- A second console instance overwrote the file (only one should run).

## The output

### `Input Rate: 0/s` in VRChat

| Cause | Fix |
|---|---|
| OSC disabled in VRChat | **Options → OSC → Enabled** |
| Wrong ports | `9001` receive, `9000` send — see [Ports](ports.md) |
| Firewall blocking UDP `9001` | Allow on private networks |
| VRChat custom launch options | Add `--osc=9000:127.0.0.1:9001` |

### `Input Rate` > 0, `Output Rate: 0/s`

- Trackers produce nothing: check `FPS`/`PPS` and [Home](../software/home.md) pills.
- **VRC Direct** is off (intentionally, if you use an external module).
- A module with higher priority took ownership — check **Detected DLLs** on
  [VRCFT](../software/vrcft.md).

### Avatar detected, but expressions do not move

- Amplitude set to `0` for those shapes on [Expression Amplitude](../software/expression-amplitude.md).
- The avatar lacks the parameter names.
- The avatar's own "face tracking" toggle is off in its menu.

### External VRCFaceTracking module shows no data

Almost always: **VRC Direct is still on**. Turn it off; the console only emits compatibility packets
in that state. See [External VRCFT](../guides/external-vrcft.md).

## Quality

### Gaze drifts left/right over a session

The mount is moving. Tighten it, then **Recenter Now**. If it still drifts, check whether the headset
straps are loose.

### Gaze offset differs between the eyes

One camera is aimed or focused differently. Compare the two previews side by side; the iris should sit
at a similar position at rest.

### Blinks incomplete

- Raise **Blink Close Amplitude** on [Eye](../software/eye.md).
- Recenter to refresh eyelid baselines.
- Check eyelid visibility in the preview — if the lid is out of frame, re-aim.

### Mouth shapes exaggerated or twitchy

- Lower the specific slider on [Expression Amplitude](../software/expression-amplitude.md).
- Raise **Filter Strength** on the mouth page.
- For mono builds, accept weaker `CheekPuff` / `Jaw Fwd` rather than overdriving them.

### Everything lags about 200 ms

- **Filter Strength** / **Eye Gaze Filter** too high.
- Wi-Fi congestion: lower resolution or move to 5 GHz.
- Inference on the wrong GPU — see [Face Settings](../software/face-settings.md).

## Escalation

If nothing here fits:

1. Reproduce once with a fresh console start.
2. Copy the log from [Logs](../software/logs.md).
3. File it through [Feedback](../software/feedback.md) with hardware, version and steps.

## Documentation status

The upstream Feishu wiki is not publicly readable, so this repository reconstructs the structure from
the shipped application, the public repositories and the screenshot set. When a page here disagrees
with your build, the build wins — and a note in the issue tracker is the fastest way to get the page
fixed. Sections most likely to lag behind a release:

| Area | Risk |
|---|---|
| Firmware profile names | New boards add profiles |
| Detected DLL list | Depends on what you have installed |
| Feature toggles inside **Expand** panels | Their contents change often |
| Language coverage | Partially translated builds |

---

**Next:** [FAQ](faq.md) · [Glossary](glossary.md)

<sub>[Русская версия](../../ru/reference/troubleshooting.md) · English</sub>
