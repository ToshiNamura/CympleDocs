---
title: VRChat setup
description: Enable OSC, expose avatar parameters and get Cymple data onto your avatar.
tags: [guide, vrchat, avatar]
updated: 2026-11-10
---

# VRChat setup

Tracking in the console is only half the job; the avatar has to accept the parameters. This page
covers the VRChat side for both delivery paths.

## 1. Enable OSC in VRChat

**Action Menu → Options → OSC → Enabled** (or the equivalent in the current VRChat build).

That single toggle lets VRChat send its parameter stream (so the console can detect the avatar) and
receive tracking data.

## 2. Confirm the ports

| Direction | Default port | Owner |
|---|---|---|
| VRChat → apps (its *output*) | `9001` | Cymple listens here |
| Apps → VRChat (its *input*) | `9000` | Cymple sends here |

If nothing arrives, add the launch option from [OSC Router](../software/osc-router.md):

```text
--osc=9000:127.0.0.1:9001
```

Steam → **VRChat → Properties → General → Launch Options**, then restart VRChat.

## 3. Avatar parameters

Cymple drives the standard VRCFaceTracking-compatible parameter set: 28 expressions plus eye and
gaze values. Your avatar must expose parameters with matching names.

### Via VRCFaceTracking (recommended for avatars already set up for face tracking)

1. Add [VRCFaceTracking](https://vrcft.io) to the Unity project (VRCFT's Avatar Setup / Unified
   Expressions).
2. Run its setup on your avatar and let it create the parameter list and animations.
3. Upload the avatar.
4. In game, confirm `Face Tracking` / OSC parameters are not blocked by the avatar's own menu.

### Via VRC Direct

VRC Direct writes OSC parameters directly. The avatar still needs the parameters and the animation
layers to consume them — Cymple supplies data, not the rig. If your avatar was built for VRCFT, it
already has them.

## 4. Common parameter names

Names follow the VRCFT/VRChat conventions:

| Domain | Examples |
|---|---|
| Eyes | `EyeLeft`, `EyeRight`, `EyeLidLeft`, `EyeLidRight`, `PupilDilation` |
| Expressions | `JawOpen`, `MouthClosed`, `Smile`, `BrowDownLeft`, `CheekPuff`, … |

The exact casing matters. The list in [Expression Amplitude](../software/expression-amplitude.md) is
the console's own naming; map it to your avatar's parameter names in the animator, or use a VRCFT
avatar setup that already does.

## 5. Test in game

1. Start the console, then SteamVR, then VRChat.
2. Open a private world with a mirror.
3. Blink — eyelids should respond.
4. Look left/right — pupils should move.
5. Smile, open your jaw, puff your cheeks.
6. If nothing moves, watch [VRCFT](../software/vrcft.md) → **Output Rate**.

## 6. Per-avatar amplitudes

Once VRChat reports the avatar, the red **Current avatar not detected** banner on
[Expression Amplitude](../software/expression-amplitude.md) disappears, and edits apply to that
avatar's profile. Load each avatar you use, tune it once, and the console remembers.

## Troubleshooting

| Symptom | Check |
|---|---|
| Avatar never detected by the console | OSC off in game, wrong ports, firewall |
| Some expressions never move | Parameter missing on the avatar, or amplitude at `0` |
| Expressions move the wrong way | Animator mapping, not the tracker — test with the mirror and the console's output |
| Eyes move, mouth does not | Mouth tracker offline, or `Face Tracking` disabled on [Home](../software/home.md) |
| Everything works for minutes then stops | Wi-Fi drop — see [Network setup](../hardware/network.md) |

## Safety settings worth knowing

- VRChat's **OSC Debug** panel is the fastest way to see whether parameters arrive at all.
- Some avatars ship with a "face tracking off" toggle in their menu; make sure it is on.
- Moderation/report systems are unaffected — Cymple only feeds parameters.

---

**Next:** [External VRCFT](external-vrcft.md) · [Expression Amplitude](../software/expression-amplitude.md)

<sub>[Русская версия](../../ru/guides/vrchat-setup.md) · English</sub>
