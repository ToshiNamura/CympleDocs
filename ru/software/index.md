---
title: Справочник по консоли
description: Макет окна, навигация и общие соглашения интерфейса консоли Cymple.
tags: [software, ui]
updated: 2026-11-10
---

# Справочник по консоли

**Консоль Cymple** — панель управления всеми модулями в Windows. В этом разделе она разобрана
страница за страницей и элемент за элементом по макету версии 4.20.2.

## Макет окна

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

### Боковая панель

- **Home**, **Logs**, **Global Settings**, **Feedback** — плоские пункты.
- **Cympleface** — сворачиваемая группа, в которой собраны страницы трекинга и инструменты устройства.
- Активная страница подсвечена светлым фоном и синей полосой слева.
- Настройки, которые относятся к устройству, а не к аватару, живут в **Cympleface**; настройки
  самого приложения — внизу боковой панели. Разделение намеренное, и о нём стоит помнить, когда
  ищете нужный параметр.

### Заголовок окна

| Элемент | Действие |
|---|---|
| ☀ (солнце) | Быстрое переключение темы |
| ⚙ (шестерёнка) | Открывает [Global Settings](global-settings.md) |
| — / □ / × | Свернуть, развернуть, закрыть. Кнопка закрытия подчиняется параметру **Window Close Action** в Global Settings |

### Общие приёмы

| Приём | Значение |
|---|---|
| Зелёная плашка **Enabled** | Подсистема работает и выдаёт данные |
| Серая плашка / *Off* | Подсистема отключена |
| Кнопка **Expand ⌄** | Раскрывает панель, свёрнутую ради экономии места ([Record Dataset](eye.md), **Eye Special Toggle Settings**) |
| Ползунок с числовым полем | В поле можно ввести точное значение; ползунок даёт только грубую настройку |
| Значок ⟲ справа от ползунка | Сбрасывает это значение к значению по умолчанию |
| Предпросмотр + `FPS` / `PPS` | Живое изображение и счётчики в секунду: кадры и обработанные отсчёты |
| **Save and apply** | Только на [OSC Router](osc-router.md) — всё остальное применяется сразу |

## Страницы

| Страница | Файл |
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

## Где хранятся настройки

Всё сохраняется в `%LOCALAPPDATA%\Cymple\iniFile.ini`, а для старых установок есть запасной путь
`C:\Cymple\iniFile.ini`. См. [Файл конфигурации](../reference/config.md).

## Различия версий

Версия напечатана в заголовке окна и повторяется в первой строке [Logs](logs.md). Если страница не
совпадает с этой документацией, баннер в журнале — самый быстрый способ понять, какая сборка перед
вами.

---

**Далее:** [Home](home.md) · [Eye](eye.md)

<sub>[English version](../../en/software/index.md) · Русский · ИИ-перевод: DeepSeek-V4.1--Flash</sub>
