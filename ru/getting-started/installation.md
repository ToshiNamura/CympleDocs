---
title: Установка
description: Установите Cymple Console, драйвер SteamVR и необязательный модуль VRCFaceTracking.
tags: [install, steamvr, vrcft]
updated: 2026-11-10
---

# Установка

Три компонента устанавливаются независимо. Делайте это в указанном порядке: каждый шаг можно
проверить, прежде чем двигаться дальше.

## 1. Cymple Console

1. Скачайте актуальную сборку консоли (4.20.x на момент написания).
2. Запустите установщик или распакуйте портативный ZIP в путь **без** символов вне ASCII
   (`C:\Cymple` — классическое место, оно до сих пор используется как резервный путь к конфигу).
3. Запустите приложение. В заголовке окна — название продукта и версия, `Cymple 4.20.2` на наших
   снимках.
4. При первом запуске Windows Firewall спросит доступ к сети. **Разрешите его для частных сетей**;
   без этого консоль не увидит камеры, и вы будете видеть только *Waiting for image*.

### Что создаётся

| Путь | Содержимое |
|---|---|
| `%LOCALAPPDATA%\Cymple\iniFile.ini` | Все настройки консоли, включая параметры отдельных аватаров |
| `%LOCALAPPDATA%\Cymple\logs\` | `log_YYYY-MM-DD_HH-MM-SS.txt`, один файл на сеанс |
| `C:\Cymple\iniFile.ini` | Устаревший резервный путь; читается модулем VRCFT, если нового файла нет |
| `%LOCALAPPDATA%\Cymple\datasets\` | Записи датасетов (по желанию) |

О ключах, которые действительно важны, см. [Файл конфигурации](../reference/config.md).

## 2. Драйвер OpenVR (SteamVR)

Драйвер делает трекер видимым для SteamVR и позволяет консоли запускаться и закрываться вместе с
рантаймом.

1. Закройте SteamVR.
2. Скопируйте папку `cymple` (внутри `driver_cymple.dll` и `driver.vrdrivermanifest`) в:

   ```text
   C:\Program Files (x86)\Steam\steamapps\common\SteamVR\drivers\cymple\
   ```

3. Запустите SteamVR. Откройте **Settings → Startup / Shutdown → Manage Add-ons** и убедитесь, что
   в списке есть *cymple* и он включён.
4. По желанию: в [Global Settings](../software/global-settings.md) оставьте включённым **Start and
   close with SteamVR**, чтобы консоль следовала за рантаймом, а не запускалась вручную.

Если SteamVR отказывается загружать драйвер, поищите строки `driver_cymple` в
`SteamVR/logs/vrserver.txt` и проверьте, что DLL не заблокирована (правый клик →
**Properties → Unblock**).

## 3. Модуль VRCFaceTracking (необязательно)

Пропустите этот раздел, если собираетесь использовать только **VRC Direct**.

1. Установите [VRCFaceTracking](https://vrcft.io).
2. Скачайте ZIP релиза `CympleFaceTracking` — внутри `CympleFaceTracking.dll` и метаданные модуля.
3. В VRCFaceTracking откройте **Module Manager → Custom modules → Install from file** и выберите ZIP
   (или положите DLL в папку модулей и перезапустите).
4. Убедитесь, что модуль появился как **Cymple Module** с активными доменами взгляда и мимики.
5. В консоли выключите **VRC Direct** (см. [VRCFT](../software/vrcft.md)) — пакеты совместимости,
   нужные модулю, отправляются только при отключённом прямом режиме.

> Модуль читает из INI консоли единственную настройку:
> `[Cymple_Mouth] reset_expression_on_tracking_disconnect`. Всё остальное — доступность доменов
> взгляда и рта, приоритеты, включение и выключение — управляется самим VRCFaceTracking.

## 4. Проверка установки

| Проверка | Ожидаемый результат |
|---|---|
| Консоль открывается, боковая панель отрисована | Доступны все двенадцать страниц |
| [Home](../software/home.md) показывает три зелёные плашки **Enabled** | Eye Tracking, Face Tracking и VRCFT включены |
| В [Logs](../software/logs.md) есть строка с версией | `Cymple software version: 4.20.2` |
| Список дополнений SteamVR | Драйвер *cymple* включён |
| Список модулей VRCFT | Присутствует *Cymple Module* (только при внешнем VRCFT) |

## Удаление

1. Выключите **Start and close with SteamVR** и закройте консоль.
2. Удалите `SteamVR\drivers\cymple\`.
3. Удалите модуль из VRCFaceTracking.
4. Удалите консоль; при желании удалите `%LOCALAPPDATA%\Cymple`, чтобы стереть настройки, журналы и
   датасеты.

---

**Далее:** [Быстрый старт](quick-start.md) · [Настройка сети](../hardware/network.md)

<sub>[English version](../../en/getting-started/installation.md) · Русский · ИИ-перевод: DeepSeek-V4.1--Flash</sub>
