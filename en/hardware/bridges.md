---
title: Third-party bridges
description: Use Cymple with other eye and face trackers through the bundled bridge tools.
tags: [hardware, integration, bridges]
updated: 2026-11-10
---

# Third-party bridges

Cymple speaks OSC on the outside, which makes it a natural hub: you can feed it data from another
tracker and let the console do the expression solving and routing.

The repository ships two bridge utilities in `混搭软件/`:

| Tool | Direction | Purpose |
|---|---|---|
| `BrokenEye2Cymple.exe` | Third-party tracker → Cymple | Receives another eye tracker's output and re-emits it as Cymple-understood data |
| `Bsb2E to Cymple Bridge.exe` | Expression source → Cymple | Converts an expression stream into Cymple's input format so the console's output path can carry it |

Both are standalone executables — no installer, no service.

## Typical mixed setup

```text
Another eye tracker ──► BrokenEye2Cymple ──► Cymple Console ──► VRChat
(maker-specific OSC)        (protocol bridge)     (filters, OSC out)
```

Why bother? You keep the console's filtering, per-avatar amplitude profiles and OSC Router
forwarding, while using hardware it does not natively drive.

## Rules

1. **One owner per port.** If the bridge listens on the same port the console uses, the console
   loses. Check [Ports and endpoints](../reference/ports.md) and move one side.
2. **Turn VRC Direct off** while you are still wiring a bridge; it makes the data path explicit and
   keeps you from chasing the wrong link.
3. **Verify with the console's own counters.** [VRCFT](../software/vrcft.md) shows **Input Rate** and
   **Output Rate**. If input moves and output does not, the bridge is fine and the problem is
   downstream.
4. **Document your chain.** Mixed setups are the hardest to support; keep a note of which tool feeds
   which port.

## Limits

- Bridges translate protocols, not sensor physics. A 30 FPS tracker stays a 30 FPS tracker.
- Expression bridges cannot invent expressions the source does not produce; missing shapes stay at
  zero.
- Support for third-party tools is best-effort — they are community utilities, not shipped features.

---

**Next:** [Ports and endpoints](../reference/ports.md) · [OSC Router](../software/osc-router.md)

<sub>[Русская версия](../../ru/hardware/bridges.md) · English</sub>
