# Cymple Docs / Документация Cymple

Bilingual product documentation for the **Cymple** eye- and face-tracking ecosystem.
Двуязычная документация продуктов **Cymple** — отслеживание взгляда и мимики.

> ⚠️ **AI-assisted translation / Перевод выполнен с помощью ИИ**
>
> The Russian documentation in `ru/` was translated by the AI model **DeepSeek-V4.1--Flash** and may
> contain inaccuracies, awkward phrasing or outdated wording. The English pages in `en/` are the
> source of truth, and the application itself overrides both: when a page disagrees with the console,
> trust the console. Native-speaker review of the Russian text is welcome — see
> [Contributing](#contributing--участие).
>
> Русская документация в `ru/` переведена моделью **DeepSeek-V4.1--Flash** и может содержать
> неточности, стилистические огрехи или устаревшие формулировки. Источник истины — английские
> страницы в `en/`, а если страница расходится с самой программой, верьте программе. Вычитка
> носителем языка приветствуется — см. [Участие](#contributing--участие).

| Language / Язык | Entry point / Точка входа |
|---|---|
| English | [`en/index.md`](en/index.md) |
| Русский | [`ru/index.md`](ru/index.md) |

## What is covered / Что описано

- **Cymple Console 4.20.x** — the Windows application that drives every tracking module.
- **CympleFace modules** — Eye Tracking, Face Tracking (dual-camera and single-camera mouth), Expression Amplitude, VRCFT relay.
- **Hardware** — DIY eye tracker and mouth trackers built on ESP32 camera modules, network setup, firmware flashing.
- **Integration guides** — VRChat OSC, VRCFaceTracking, OSC Router forwarding, calibration and dataset recording.

## Repository layout / Структура репозитория

```text
.
├── README.md                 this file
├── mkdocs.yml                optional static-site build
├── assets/screenshots/       console screenshots used by both languages
├── en/                       English wiki
│   ├── index.md
│   ├── getting-started/      overview, requirements, install, quick start
│   ├── hardware/             devices, network, firmware
│   ├── software/             page-by-page console reference
│   ├── guides/               VRChat, calibration, dataset recording
│   └── reference/            ports, config file, troubleshooting, FAQ, glossary
└── ru/                       Russian wiki (mirror of en/)
```

## Conventions / Соглашения

- Every page starts with a front-matter block (`title`, `description`, `tags`, `updated`).
- UI labels are quoted exactly as they appear in the console, e.g. **Output smoothing**.
- Values that appear in screenshots are marked as *defaults* and are not hard requirements.
- Cross-links use relative paths so the docs render on GitHub, in VS Code and in MkDocs.

## Sources / Источники

- Upstream project: [Dominocs/Project_Cymple](https://github.com/Dominocs/Project_Cymple) (hardware, firmware, DIY tutorials).
- VRCFT module: [Dominocs/CympleFaceTracking](https://github.com/Dominocs/CympleFaceTracking).
- Console screenshots: attached by the product owner, Cymple Console 4.20.2, 1920×1080.

> The original Feishu wiki is behind a login wall, so this repository reconstructs and expands its structure from the shipped application, the public repositories and the screenshot set. See [en/reference/troubleshooting.md](en/reference/troubleshooting.md) for the documentation gap policy.

## Contributing / Участие

Priority fixes, in order:

1. **UI labels and term names** in `ru/` that do not match the Russian build of the console.
2. **Translation errors** — mistranslated tooltips, wrong port numbers or defaults.
3. **Rendering problems** — broken tables, links or screenshots on GitHub.

Please keep both languages in sync: a change to `en/…` needs the matching change in `ru/…`. If you
only fix one language, say so in the pull request so the gap is tracked.

Приоритет правок:

1. **Названия элементов интерфейса и термины** в `ru/`, которые не совпадают с русской сборкой консоли.
2. **Ошибки перевода** — неверно переданные подсказки, номера портов или значения по умолчанию.
3. **Проблемы отображения** — сломанные таблицы, ссылки или скриншоты на GitHub.

Держите оба языка синхронными: изменение в `en/…` требует парного изменения в `ru/…`. Если правите
только один язык, укажите это в pull request, чтобы расхождение было видно.

## License / Лицензия

This repository contains documentation, not code. No licence is granted by default: the repository
owner decides how the text may be reused. Screenshots of the Cymple Console belong to the Cymple
project; hardware models, firmware and upstream code follow the licences of their source
repositories.

Репозиторий содержит документацию, а не код. По умолчанию лицензия не предоставляется: порядок
переиспользования текста определяет владелец репозитория. Скриншоты Cymple Console принадлежат
проекту Cymple; модели, прошивки и код проекта распространяются по лицензиям исходных репозиториев.

