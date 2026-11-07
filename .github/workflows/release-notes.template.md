# Русский

Форк-сборка эмулятора Korg MS2000R поверх апстрима v__BASE__. Выпущено __DATE__.

> **Внимание:** эта версия — **только для Windows (x64)**.

**Апстрим-версия:** [Tuth/ms2000r-emu v__BASE__](https://github.com/Tuth/ms2000r-emu).

## Изменения относительно апстрима v__BASE__

- **Сохранение состояния плагина исправлено** — пресеты теперь надёжно сохраняются и восстанавливаются в проекте DAW (PR #8).
- **Исправлены пропорции окна редактора** — панель сохраняет правильное соотношение сторон в рамках мин/макс размеров (PR #11).
- **Добавлена опция `Report latency to host`** в настройках — хост получает корректную задержку плагина (PR #12).

## Соглашения форка

- Суффикс версии `-paulhuman.<n>` отличает форк-сборки (например, `v0.9.8-paulhuman.1`).
- Бандл VST3 поставляется как папка `MS2000R.vst3/` — её можно положить прямо в каталог VST3.
- Сборка и упаковка выполняются автоматически через GitHub Actions.

## Установка

- Распакуйте архив `MS2000R-v__VER__-win64.zip` и скопируйте папку `MS2000R.vst3` в каталог VST3 вашего хоста (например, `C:\Program Files\Common Files\VST3`).
- Убедитесь, что у вас есть необходимые ROMs/прошивки (см. README).

---

# English

Fork build of the Korg MS2000R emulator on top of upstream v__BASE__. Released __DATE__.

> **Note:** this build is **Windows-only (x64)**.

**Upstream version:** [Tuth/ms2000r-emu v__BASE__](https://github.com/Tuth/ms2000r-emu).

## Changes vs upstream v__BASE__

- **Plugin state recall fixed** — presets now save and restore reliably in the DAW project (PR #8).
- **Editor window proportions fixed** — the panel keeps the correct aspect ratio within min/max bounds (PR #11).
- **Added `Report latency to host` option** in settings — the host now receives the plugin's correct latency (PR #12).

## Fork conventions

- A `-paulhuman.<n>` version suffix marks fork builds (e.g. `v0.9.8-paulhuman.1`).
- The VST3 bundle ships as an `MS2000R.vst3/` folder — drop it straight into your VST3 directory.
- Builds and packaging are automated via GitHub Actions.

## Installation

- Unzip `MS2000R-v__VER__-win64.zip` and copy the `MS2000R.vst3` folder into your host's VST3 directory (e.g. `C:\Program Files\Common Files\VST3`).
- Make sure you have the required ROMs/firmware (see README).
