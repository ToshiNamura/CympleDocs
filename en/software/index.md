---
title: Console reference
description: Layout, navigation and shared conventions of the Cymple Console UI.
tags: [software, ui]
updated: 2026-11-10
---

# Console reference

The Cymple Console is the Windows control surface for every module. This section documents it page
by page, control by control, using the 4.20.2 layout.

## Window layout

```text
┌──────────────────────────────────────────────────────────────────────┐
│ Cymple 4.20.2            [☀] [⚙] [—] [□] [×]                         │  title bar
├─────────────────────┬────────────────────────────────────────────────┤
│ Home                │                                                │
│ ▾ Cympleface        │        page content                            │
│    Eye              │        (two or three columns of cards)         │
│    Dual-Camera …    │                                                │
│    Single-Camera …  │                                                │
│    Expression …     │                                                │
│    VRCFT            │                                                │
│    Face Settings    │                                                │
│    Firmware Flash   │                                                │
│    OSC Router       │                                                │
│                     │                                                │
│ Logs                │                                                │
│ Global Settings     │                                                │
│ Feedback            │                                                │
└─────────────────────┴────────────────────────────────────────────────┘
```

### Sidebar

- **Home**, **Logs**, **Global Settings**, **Feedback** are flat entries.
- **Cympleface** is a collapsible group holding the tracking pages and device tools.
- The active page is highlighted with a light background and a blue left bar.
- Settings that belong to the device rather than the avatar live in **Cympleface**; settings that
  belong to the application live at the bottom of the sidebar. That split is deliberate and worth
  remembering when you look for an option.

### Title bar

| Control | Action |
|---|---|
| ☀ (sun) | Theme switch shortcut |
| ⚙ (gear) | Opens [Global Settings](global-settings.md) |
| — / □ / × | Minimise, maximise, close. The close button follows **Window Close Action** in Global Settings |

### Shared patterns

| Pattern | Meaning |
|---|---|
| Green pill **Enabled** | Subsystem running and producing data |
| Grey pill / *Off* | Subsystem disabled |
| **Expand ⌄** button | Reveals a panel that is collapsed to save space ([Record Dataset](eye.md), **Eye Special Toggle Settings**) |
| Slider row with a numeric box | Text entry accepts exact values; the slider is coarse |
| ⟲ icon at the right of a slider | Reset that value to its default |
| Preview + `FPS` / `PPS` | Live image and per-second counters: frames, and processed samples |
| **Save and apply** | Only on [OSC Router](osc-router.md) — everything else applies immediately |

## Pages

| Page | File |
|---|---|
| Home | [home.md](home.md) |
| Eye | [eye.md](eye.md) |
| Dual-Camera Mouth | [dual-camera-mouth.md](dual-camera-mouth.md) |
| Single-Camera Mouth | [single-camera-mouth.md](single-camera-mouth.md) |
| Expression Amplitude | [expression-amplitude.md](expression-amplitude.md) |
| VRCFT | [vrcft.md](vrcft.md) |
| Face Settings | [face-settings.md](face-settings.md) |
| Firmware Flash | [firmware-flash.md](firmware-flash.md) |
| OSC Router | [osc-router.md](osc-router.md) |
| Logs | [logs.md](logs.md) |
| Global Settings | [global-settings.md](global-settings.md) |
| Feedback | [feedback.md](feedback.md) |

## Where settings are stored

Everything is persisted in `%LOCALAPPDATA%\Cymple\iniFile.ini`, with a legacy fallback at
`C:\Cymple\iniFile.ini`. See [Configuration file](../reference/config.md).

## Version differences

The version is printed in the title bar and repeated in the first [Logs](logs.md) line. When a page
does not match this documentation, the log banner is the fastest way to confirm which build you are
looking at.

---

**Next:** [Home](home.md) · [Eye](eye.md)

<sub>[Русская версия](../../ru/software/index.md) · English</sub>
