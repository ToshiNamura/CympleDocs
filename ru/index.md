---
title: Вики Cymple
description: Документация по отслеживанию взгляда и мимики Cymple и консоли Cymple Console.
tags: [home]
updated: 2026-11-10
---

# Вики Cymple

**Cymple** — недорогая открытая система отслеживания взгляда и мимики для VR. Пара небольших
камер на ESP32 передаёт кадры по Wi-Fi в **Cymple Console**, которая превращает изображение в
направление взгляда и 28 выражений лица и отдаёт результат в VRChat — напрямую (VRC Direct + OSC)
или через VRCFaceTracking.

> ⚠️ **Перевод выполнен с помощью ИИ.** Русская версия документации переведена моделью
> **DeepSeek-V4.1--Flash** и может содержать неточности, стилистические огрехи и устаревшие
> формулировки. Источник истины — английская версия ([en/index.md](../en/index.md)), а если текст
> расходится с самой программой, верьте программе. Вычитка носителем языка приветствуется:
> ошибки в терминах и названиях элементов интерфейса исправляются в первую очередь.

В этой вики три части:

1. **Железо** — что собрать, как напечатать корпус и как вывести устройство в сеть.
2. **Программа** — каждая страница консоли, каждый переключатель.
3. **Интеграция** — как довести данные до VRChat и до аватара.

## С чего начать

| Если вы хотите… | Читайте |
|---|---|
| Понять, что Cymple умеет, а что нет | [Обзор](getting-started/overview.md) |
| Проверить требования к ПК, шлему и сети | [Требования](getting-started/requirements.md) |
| Установить консоль, драйвер и модуль | [Установка](getting-started/installation.md) |
| Получить работающий трекинг за 15 минут | [Быстрый старт](getting-started/quick-start.md) |
| Собрать айтрекер | [Айтрекер](hardware/eye-tracker.md) |
| Собрать трекер мимики | [Две камеры](hardware/dual-camera-mouth.md) · [Одна камера](hardware/single-camera-mouth.md) |
| Настроить Wi-Fi и IP устройства | [Настройка сети](hardware/network.md) |
| Прошить устройство | [Прошивка](hardware/firmware.md) |

## Справочник по консоли

Приложение организовано как плоское боковое меню: **Home**, затем группа **Cympleface**, затем
**Logs**, **Global Settings** и **Feedback**.

| Страница | Назначение |
|---|---|
| [Home](software/home.md) | Переключатели модулей: Eye Tracking, Face Tracking, VRCFT |
| [Eye](software/eye.md) | Предпросмотры камер, IP, калибровка, фильтры, амплитуды взгляда и зрачка |
| [Dual-Camera Mouth](software/dual-camera-mouth.md) | Стереотрекинг мимики, сшивка, диапазон камеры |
| [Single-Camera Mouth](software/single-camera-mouth.md) | Монокулярный трекинг с ручным ROI |
| [Expression Amplitude](software/expression-amplitude.md) | Усиление по каждому блендшейпу, 28 ползунков |
| [VRCFT](software/vrcft.md) | VRC Direct, порты, менеджер плагинов, приоритеты |
| [Face Settings](software/face-settings.md) | Устройство вывода (GPU), сброс выражения при обрыве |
| [Firmware Flash](software/firmware-flash.md) | Профиль прошивки, COM-порт, журнал прошивки |
| [OSC Router](software/osc-router.md) | Пересылка OSC на телефоны, трекеры и другие приложения |
| [Logs](software/logs.md) | Просмотр журнала работы |
| [Global Settings](software/global-settings.md) | Язык, тема, запуск вместе со SteamVR |
| [Feedback](software/feedback.md) | Отчёты об ошибках и предложения |

## Руководства

- [Калибровка](guides/calibration.md) — точная калибровка, перецентровка, диапазонная калибровка.
- [Запись датасета](guides/dataset-recording.md) — сбор собственных данных для обучения.
- [Настройка VRChat](guides/vrchat-setup.md) — OSC, параметры аватара, VRCFT вне консоли.
- [Внешний VRCFT](guides/external-vrcft.md) — модуль внутри VRCFaceTracking вместо VRC Direct.

## Справочник

- [Порты и адреса](reference/ports.md)
- [Файл конфигурации](reference/config.md)
- [Диагностика проблем](reference/troubleshooting.md)
- [Частые вопросы](reference/faq.md)
- [Глоссарий](reference/glossary.md)

## О версии

Скриншоты в вики сняты в **Cymple Console 4.20.2**. Названия и значения по умолчанию меняются от
релиза к релизу; если элемента нет в вашей сборке, посмотрите баннер версии в
[Logs](software/logs.md) и сравните с примечаниями к выпуску.

---

<sub>[English version](../en/index.md) · Русский</sub>
