---
title: Installation
description: Install the Cymple Console, the SteamVR driver and the optional VRCFaceTracking module.
tags: [install, steamvr, vrcft]
updated: 2026-11-10
---

# Installation

Three components install independently. Do them in this order; each step is verifiable before you
move on.

## 1. Cymple Console

1. Download the current console build (4.20.x at the time of writing).
2. Run the installer, or unpack the portable ZIP to a path **without** non-ASCII characters
   (`C:\Cymple` is the classic location and is still used as a config fallback).
3. Launch it. The title bar shows the product name and version — `Cymple 4.20.2` in our captures.
4. On first launch Windows Firewall asks for network access. **Allow it on private networks**;
   without it the console cannot reach the cameras and you will only ever see
   *"Waiting for image"*.

### What gets created

| Path | Content |
|---|---|
| `%LOCALAPPDATA%\Cymple\iniFile.ini` | All console settings, including per-avatar parameters |
| `%LOCALAPPDATA%\Cymple\logs\` | `log_YYYY-MM-DD_HH-MM-SS.txt`, one file per session |
| `C:\Cymple\iniFile.ini` | Legacy fallback, read by the VRCFT module if the new path is absent |
| `%LOCALAPPDATA%\Cymple\datasets\` | Optional dataset recordings |

See [Configuration file](../reference/config.md) for the keys that matter.

## 2. OpenVR driver (SteamVR)

The driver makes SteamVR aware of the tracker and lets the console start/stop with the runtime.

1. Close SteamVR.
2. Copy the folder `cymple` (containing `driver_cymple.dll` and `driver.vrdrivermanifest`) into:

   ```text
   C:\Program Files (x86)\Steam\steamapps\common\SteamVR\drivers\cymple\
   ```

3. Start SteamVR. Open **Settings → Startup / Shutdown → Manage Add-ons** and confirm
   *cymple* is listed and enabled.
4. Optional: in [Global Settings](../software/global-settings.md) keep **Start and close with
   SteamVR** on, so the console follows the runtime instead of being launched by hand.

If SteamVR refuses to load the driver, check `SteamVR/logs/vrserver.txt` for `driver_cymple` lines
and verify that the DLL is not blocked (right-click → **Properties → Unblock**).

## 3. VRCFaceTracking module (optional)

Skip this if you plan to use **VRC Direct** only.

1. Install [VRCFaceTracking](https://vrcft.io).
2. Download the `CympleFaceTracking` release ZIP — it contains `CympleFaceTracking.dll` plus module
   metadata.
3. In VRCFaceTracking open **Module Manager → Custom modules → Install from file** and pick the ZIP
   (or drop the DLL into the modules folder and restart).
4. Confirm the module appears as **Cymple Module** with eye and face domains active.
5. In the console, turn **VRC Direct** *off* (see [VRCFT](../software/vrcft.md)) — the compatibility
   packets the module needs are only sent while direct mode is disabled.

> The module reads only one preference from the console's INI:
> `[Cymple_Mouth] reset_expression_on_tracking_disconnect`. Everything else — availability of eye
> and mouth domains, priorities, enable/disable — is controlled by VRCFaceTracking itself.

## 4. Verify the install

| Check | Expected result |
|---|---|
| Console opens, sidebar renders | All twelve pages reachable |
| [Home](../software/home.md) shows three green **Enabled** pills | Eye Tracking, Face Tracking, VRCFT all on |
| [Logs](../software/logs.md) contains a version banner | `Cymple software version: 4.20.2` |
| SteamVR add-on list | *cymple* driver enabled |
| VRCFT module list | *Cymple Module* present (only if using external VRCFT) |

## Uninstalling

1. Turn off **Start and close with SteamVR** and exit the console.
2. Delete `SteamVR\drivers\cymple\`.
3. Remove the module from VRCFaceTracking.
4. Uninstall the console; optionally delete `%LOCALAPPDATA%\Cymple` to drop settings, logs and
   datasets.

---

**Next:** [Quick start](quick-start.md) · [Network setup](../hardware/network.md)

<sub>[Русская версия](../../ru/getting-started/installation.md) · English</sub>
