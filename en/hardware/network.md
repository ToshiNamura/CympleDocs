---
title: Network setup
description: Put Cymple cameras on Wi-Fi with stable IPs and keep the console able to reach them.
tags: [hardware, network, wifi]
updated: 2026-11-10
---

# Network setup

Cymple cameras are tiny web servers. If the console cannot `GET` an image from `http://<ip>/`, you
get *"Waiting for image"* and nothing else works. This page fixes that class of problem once.

## How a camera joins the network

```text
camera boots → reads stored SSID/password → joins Wi-Fi → gets IP (DHCP or static)
             → starts MJPEG server → waits for the console to pull frames
```

Two things must therefore be true:

1. The camera is on a Wi-Fi network the **PC can reach**.
2. The camera keeps **the same IP** across reboots, because the console stores the IP, not a hostname.

## Step 1 — Configure Wi-Fi credentials

Depending on the firmware build, credentials are set either by a captive portal or by the flashing
tool:

- **Captive portal builds:** connect to the camera's own access point (SSID usually starts with
  `Cymple` or the board name), open the configuration page, enter your SSID and password, save, and
  the device reboots into station mode.
- **Config-at-flash builds:** the SSID/password are written together with the firmware in the flash
  tool. Reflash to change them.

After the reboot the cameras should appear in your router's client list.

## Step 2 — Make the IP stable

| Method | How | Notes |
|---|---|---|
| **DHCP reservation** (recommended) | Bind the camera's MAC address to a fixed lease in the router | Survives firmware updates, no device config needed |
| **Static IP in device** | Set address/mask/gateway on the camera | Must match your subnet; a typo means re-flashing |
| **Hostname** | Not used | The console expects a literal IP |

Choose addresses outside the router's dynamic pool to avoid collisions, e.g. `192.168.1.201–210`.

## Step 3 — Verify from the PC

```powershell
# 1. Is the host up?
Test-Connection 192.168.1.201

# 2. Is the MJPEG endpoint answering?
curl.exe -I http://192.168.1.201/

# 3. Is the port open?
Test-NetConnection 192.168.1.201 -Port 80
```

| Result | Meaning |
|---|---|
| Ping fails | Wrong IP, different subnet, or Wi-Fi association failed |
| Ping works, HTTP fails | Camera joined the network but the stream server is not running — reflash |
| Both work, console still shows "Waiting for image" | Windows Firewall is blocking the console, or the console is running in a different network profile |

## Step 4 — Windows Firewall

The console must be allowed to make outbound connections and receive replies on private networks:

1. **Windows Security → Firewall & network protection → Allow an app through firewall**.
2. Add `Cymple.exe` (or the installer's entry) and tick **Private**.
3. If you use a second NIC (a dedicated Wi-Fi dongle for VR), set that network's profile to
   **Private**, not Public — Public applies a much stricter rule set.

## Step 5 — Router hygiene

| Setting | Required state | Why |
|---|---|---|
| AP / client isolation | **Off** | Otherwise the PC cannot reach the camera at all |
| Band steering | Off or split SSIDs | Keeps the cameras on 5 GHz deliberately |
| IGMP snooping / multicast filtering | Default (do not enable) | Can break discovery in some builds |
| QoS / airtime fairness | Optional | Helps keep `FPS` stable when other devices stream |

> **Rule of thumb.** If VRChat runs smoothly but `FPS` in the previews sits at 8–12, the problem is
> the Wi-Fi link, not the CPU. Move the router, split the bands, or reduce the number of devices on
> the 2.4 GHz SSID.

## Bandwidth budget

Each camera streams MJPEG. A rough budget at 640×480 / 25 FPS is 2–6 Mbit/s per camera depending on
scene complexity. A full four-camera setup (2 eye + 2 mouth) therefore needs a stable 20 Mbit/s of
airtime — trivial on 5 GHz, marginal on a crowded 2.4 GHz channel.

## Multiple trackers on one PC

The console addresses devices by IP, so any mix works:

- Eye tracker on `192.168.1.201` / `.202`
- Mouth tracker on `192.168.1.203`
- A second tracker set for a second user on `.211` / `.212`

Only one console instance can bind the OSC ports (9000/9001/9002) on a machine, so two users need
two PCs.

---

**Next:** [Firmware](firmware.md) · [Troubleshooting](../reference/troubleshooting.md)

<sub>[Русская версия](../../ru/hardware/network.md) · English</sub>
