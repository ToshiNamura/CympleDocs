---
title: Firmware
description: Firmware profiles, flashing procedure and recovery for Cymple camera modules.
tags: [hardware, firmware, flashing]
updated: 2026-11-10
---

# Firmware

The consoles ships its own flasher: [Firmware Flash](../software/firmware-flash.md). It writes a
release binary to an ESP32 board over a serial port — no PlatformIO, no Arduino IDE.

## Before you flash

- A **data-capable** USB cable. Charge-only cables are the most common cause of "No Device Found".
- The USB-serial driver for your board: CH340, CP210x or FTDI. Device Manager must show a COM port
  without a yellow warning triangle.
- The device **not** powered from the headset at the same time. One power source only.
- The correct **Firmware Profile** for the hardware you are holding.

## Profiles

The flasher exposes one profile per board family. Our capture shows **EYE_V3**, the current eye
tracker profile.

| Profile | Target | Notes |
|---|---|---|
| `EYE_V3` | Current eye tracker boards | Use on both left and right cameras |
| Mouth profiles | Mouth tracker boards | Match single- vs dual-camera builds |
| Dongle / tracker profiles | Pre-built kits | Distributed as `.hex` in the repository's `tracker固件/` and `dongle固件/` folders |

> **Never flash a mouth profile onto an eye board** (or vice versa) to "see what happens". The
> profile changes the stream resolution, exposure and the packet layout the console expects; the
> console will connect but interpret the data wrongly, which looks like a broken tracker.

## Flashing procedure

1. Connect the board over USB.
2. Open [Firmware Flash](../software/firmware-flash.md).
3. Pick **Firmware Profile**.
4. Press **Refresh Ports** and choose the COM port in **Flash Port**.
5. Press **Start Flashing** and leave the device alone until the log says it finished.
6. Power-cycle the board once. It boots into the new firmware and rejoins Wi-Fi.

If the port list stays at **No Device Found**:

- try another cable and another USB port (prefer a rear I/O port directly on the motherboard),
- install the serial driver manually,
- hold the board's BOOT button while plugging it in to force the bootloader.

## Recovery

A board that no longer boots usually still accepts a flash:

1. Force bootloader mode (hold **BOOT**, tap **RST**, release **BOOT**).
2. Refresh ports, flash again.
3. If the port never appears, the board is likely bricked at the USB-serial chip level — swap the
   module; it is the cheapest part of the build.

For bare ESP32 modules flashed outside the console, the repository's `面捕眼追DIY固件/` folder contains
`bootloader.bin`, `partitions.bin` and `firmware.bin`, which map to the standard ESP32 flash offsets
`0x1000`, `0x8000` and `0x10000`. The ESP32 source itself is in `esp源代码/` (PlatformIO project).

## After flashing

1. Re-check the device IP — a firmware update may drop a static IP configuration.
2. Update the IP in [Eye](../software/eye.md) or the mouth page.
3. Re-run [Calibration](../guides/calibration.md). Exposure and gain defaults can change between
   firmware versions, and calibration depends on them.

## Version pinning

Keep the firmware version and the console version compatible. When you update one, update the other;
the console's [Logs](../software/logs.md) prints its own version at startup, which is the fastest way
to confirm what you are actually running.

---

**Next:** [Third-party bridges](bridges.md) · [Firmware Flash page](../software/firmware-flash.md)

<sub>[Русская версия](../../ru/hardware/firmware.md) · English</sub>
