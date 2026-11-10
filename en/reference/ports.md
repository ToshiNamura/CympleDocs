---
title: Ports and endpoints
description: Every network port Cymple uses, who owns it, and how to change it safely.
tags: [reference, network, osc]
updated: 2026-11-10
---

# Ports and endpoints

## Desktop ports

| Port | Protocol | Direction | Owner | Purpose | Configurable |
|---|---|---|---|---|---|
| `9000` | UDP (OSC) | Cymple → VRChat | VRChat | Avatar parameters in | Yes — [VRCFT](../software/vrcft.md) **Send**, [OSC Router](../software/osc-router.md) **VRCHat target → Port** |
| `9001` | UDP (OSC) | VRChat → Cymple | Cymple | VRChat's parameter output | Yes — [VRCFT](../software/vrcft.md) **Receive** |
| `9002` | UDP (OSC) | Device/app → Cymple | Cymple | Third-party injection, relayed to `9000` | Yes — [OSC Router](../software/osc-router.md) **Device input port** |
| `22999` | UDP | Cymple → VRCFT module | Cymple | Compatibility packet stream (70 fields) used when **VRC Direct** is off | No |
| ephemeral | UDP | Model→Console forward targets | target app | Whatever you add in [OSC Router](../software/osc-router.md) | Per target |

> The pairing is deliberate: VRChat's factory defaults are **receive 9000 / send 9001**, so Cymple
> uses them unchanged. If you customise VRChat, mirror the change on both sides.

## Camera endpoints

Each ESP32 camera is a tiny HTTP server.

| Endpoint | Protocol | Port | Purpose |
|---|---|---|---|
| `/` | HTTP | `80` | Landing page / status |
| MJPEG stream | HTTP | `80` (multipart) | The frames the console pulls |
| Configuration page | HTTP | `80` | Captive-portal style setup on some builds |

The console addresses cameras purely by IP; there is no discovery protocol. See
[Network setup](../hardware/network.md).

## Who may bind what

| Rule | Reason |
|---|---|
| Only one process can bind `9000`, `9001` or `9002` | Two consoles, or a console plus another OSC app on the same ports, means one of them silently loses |
| Cymple owns `9001` while the router is enabled | Other apps must receive VRChat data through a **forwarding target**, not by binding `9001` themselves |
| External VRCFaceTracking must not fight VRC Direct | Use one path; direct mode on + external module = conflicting writes |

## Checking a port on Windows

```powershell
# Who is listening?
Get-NetUDPEndpoint -LocalPort 9000,9001,9002 | Select-Object LocalAddress,LocalPort,OwningProcess

# What is that process?
Get-Process -Id <PID>

# Is anything arriving? (quick counter check)
Get-NetUDPEndpoint | Where-Object LocalPort -in 9000,9001,9002
```

## Firewall rules you actually need

| Direction | Rule |
|---|---|
| Outbound to camera IPs | Allow the console on **Private** networks |
| Inbound `9001`, `9002` | Allow on **Private** only — never expose the OSC ports to a public network |
| `Allow LAN devices` on | Only on a trusted LAN; it opens `9002` to other hosts |

## Changing ports: the safe order

1. Stop VRChat.
2. Change the console's ports ([VRCFT](../software/vrcft.md)).
3. Change VRChat's ports to match, or add the launch option
   `--osc=<vrchat-in>:<target-ip>:<vrchat-out>`.
4. Restart VRChat and confirm **Input Rate** / **Output Rate** on [VRCFT](../software/vrcft.md).
5. Only then touch [OSC Router](../software/osc-router.md) targets.

---

**Next:** [Configuration file](config.md) · [OSC Router](../software/osc-router.md)

<sub>[Русская версия](../../ru/reference/ports.md) · English</sub>
