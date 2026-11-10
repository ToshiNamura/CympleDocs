---
title: FAQ
description: Short answers to the questions that come up before and after buying or building Cymple.
tags: [reference, faq]
updated: 2026-11-10
---

# FAQ

## Buying and building

**Do I need to solder?**
No for the standard builds: camera modules come with connectors and the shells screw together. Some
lens swaps and the magnetic variants need a little work.

**Can I buy it instead of building it?**
Yes — pre-built kits exist alongside the open hardware. The console and the docs are the same.

**How much does a DIY build cost?**
The project's premise is "a fraction of a commercial tracker": two ESP32 camera modules, a printed
shell, a cable and power. Prices vary wildly by region; the repository's README is the honest source.

**Does it work with my headset?**
If there is a mount for it, or you use the universal adhesive clip. Provided: Quest 2/3/3S/Pro, Pico
4/4 Pro/4U, Pico Neo 3, Pimax Crystal, Pimax Dream Air/SE, PSVR2, universal.

## Software

**Which Windows versions are supported?**
Windows 10 64-bit (1909+) and Windows 11. The OpenVR driver and flasher are Windows-only.

**Do I need VRCFaceTracking?**
No. **VRC Direct** sends straight to VRChat. VRCFT is for mixing trackers or using its avatar tooling.

**Why does the Expression Amplitude page say "no current avatar was detected"?**
VRChat has not told the console which avatar is loaded. You are editing the default profile. Enable
OSC in VRChat and keep VRC Direct on; see
[Expression Amplitude](../software/expression-amplitude.md).

**Can I run two headsets / two users on one PC?**
No. One console instance owns the OSC ports. Two users need two PCs.

**Does the console phone home?**
It has no account system and no cloud round-trip for tracking. Bug reports are explicit and include the
config file, which you can review first.

## Tracking

**How accurate is the gaze?**
Consumer-grade. Fine for social VR and eye contact; not fine for research or biometrics. Accuracy is
dominated by fit, lighting and calibration, not by the software.

**Why does mono mouth tracking miss `CheekPuff`?**
No stereo baseline means no depth. The dual-camera build exists for exactly that reason.

**Do I have to recalibrate every session?**
Recenter: yes, it takes a second. Range calibration: no, once per mount is enough.

**Will it work in the dark?**
Only with IR illumination and an IR-pass lens. Visible-light-only builds need some light on the face.

**Does it drain the headset battery?**
The cameras draw from whatever powers them; on a Quest via USB you are adding load to the headset or
its battery strap. A separate power bank is the usual choice.

## Network

**2.4 GHz or 5 GHz?**
5 GHz strongly preferred, especially for stereo mouth. 2.4 GHz works for a single eye camera in a clean
environment.

**Do the cameras need internet?**
No. They only need to reach the PC.

**Can I use a phone hotspot?**
Yes, if client isolation is off and the PC joins the same hotspot.

## Privacy

**What is recorded?**
Only what you explicitly record with **Record Dataset**, plus normal logs. Recordings contain images of
your face.

**Are screenshots in a bug report necessary?**
No, but they shorten the diagnosis dramatically. Review the config attachment first — it contains your
local IPs.

## Contributing

**How do I report a bug well?**
Reproduce once, copy the log, describe steps and expectations. See
[Feedback](../software/feedback.md).

**Is the hardware open source?**
Yes: models, firmware and ESP32 sources are in the repository under the project's licence. The Windows
console is distributed as a built application.

---

**Next:** [Glossary](glossary.md) · [Troubleshooting](troubleshooting.md)

<sub>[Русская версия](../../ru/reference/faq.md) · English</sub>
