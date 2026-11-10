---
title: Configuration file
description: Where Cymple stores its settings, what the sections mean, and how to edit them safely.
tags: [reference, config, ini]
updated: 2026-11-10
---

# Configuration file

## Location

| Path | Role |
|---|---|
| `%LOCALAPPDATA%\Cymple\iniFile.ini` | Primary settings store |
| `C:\Cymple\iniFile.ini` | Legacy fallback, still read by the VRCFT module if the primary is missing |

Back up the file before editing. It holds device IPs, every per-avatar amplitude and the delivery
path settings — losing it means re-tuning.

## What lives there

| Group | Examples |
|---|---|
| Global | Language, theme, SteamVR lifecycle, window close action |
| Eye | Camera IPs, filter values, amplitudes, calibration state |
| Mouth | IP, range/offset/rotation, filter strength, ROI mode |
| Expressions | Per-avatar amplitude sets plus the default set |
| Output | Direct mode, OSC ports, router targets |
| Diagnostics | Log verbosity |

## Keys you may see

The exact key names change between releases; confirm them by opening your own file rather than
copying a snippet from an old guide.

| Section | Key | Meaning |
|---|---|---|
| `Cymple_Mouth` | `reset_expression_on_tracking_disconnect` | `1` resets expressions after a disconnect, `0` holds the last frame. Read by the VRCFT module once per second |
| `Cymple_Eye` | `cymple_eye_sw` | Hardware eye switch state. Cannot disable *another* application's input through the module |
| `Cymple_Mouth` | `cymple_mouth_sw` | Hardware mouth switch state, same caveat |

> The module deliberately ignores the two hardware switches when running inside VRCFaceTracking. Local
> hardware switches on one machine must not silently disable tracking on another application — that is
> a design decision, not a bug.

## Editing safely

1. **Exit the console.** It writes the file on change; editing it live loses your edits.
2. Copy `iniFile.ini` to `iniFile.backup.ini`.
3. Edit with a plain-text editor (UTF-8, no BOM).
4. Keep the INI grammar: `key=value`, one per line, `[Section]` headers in square brackets.
5. Start the console and check [Logs](../software/logs.md) for parse errors.
6. If something breaks, restore the backup.

## Reset to defaults

| Scope | How |
|---|---|
| One slider | ⟲ icon next to the value on its page |
| One page | Re-enter the documented defaults shown in this wiki |
| Everything | Exit the console, rename `iniFile.ini`, restart — a fresh file is generated |

Resetting the whole file also drops calibration, device IPs and per-avatar tuning. Prefer per-page
resets while you are diagnosing.

## Avatar-specific amplitude sets

When VRChat reports an avatar, the console keys the amplitude set to that avatar. The practical
consequence: editing amplitudes with no avatar loaded writes the **default** profile, which is what
every untuned avatar inherits. That is why the [Expression Amplitude](../software/expression-amplitude.md)
page shows a red *"Current avatar not detected"* pill — it is telling you which profile you are
actually editing.

## Sharing the file

A config file contains your local IP addresses and avatar parameter names. Treat it as personal data
before attaching it to a public issue; [Feedback](../software/feedback.md) attaches it automatically,
which is convenient and worth knowing.

---

**Next:** [Troubleshooting](troubleshooting.md) · [Ports](ports.md)

<sub>[Русская версия](../../ru/reference/config.md) · English</sub>
