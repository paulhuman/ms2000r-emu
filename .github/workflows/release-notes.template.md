# Русский

Форк эмулятора Korg MS2000R на основе upstream-версии v__BASE__.

> **Внимание:** сборка предназначена только для Windows (x64). Версия для macOS (AU) не входит в этот релиз.

**Upstream:** [Tuth/ms2000r-emu v__BASE__](https://github.com/Tuth/ms2000r-emu).

## Изменения с версии …

_Список изменений будет заполнен перед публикацией релиза._

## Соглашения форка

- Для обозначения собственных сборок используется суффикс версии `-paulhuman.<n>` (например, `v__BASE__-paulhuman.2`).
- VST3 bundle поставляется в виде каталога `MS2000R.vst3/`.
- Сборка и упаковка выполняются автоматически с помощью GitHub Actions.

## Установка

1. Распакуйте архив `MS2000R-v__VER__-win64.zip`.
2. Скопируйте каталог `MS2000R.vst3` в каталог VST3 вашего хоста (например, `C:\Program Files\Common Files\VST3`).
3. Убедитесь, что доступны необходимые ROM-файлы и прошивки (см. README исходного проекта).

---

# English

Fork of the Korg MS2000R emulator based on upstream version v__BASE__.

> **Note:** this build is intended for Windows (x64) only. A macOS (AU) version is not part of this release.

**Upstream:** [Tuth/ms2000r-emu v__BASE__](https://github.com/Tuth/ms2000r-emu).

## Changes since …

_The list of changes will be filled in before the release is published._

## Fork conventions

- Own builds are marked with a `-paulhuman.<n>` version suffix (e.g. `v__BASE__-paulhuman.2`).
- The VST3 bundle ships as a `MS2000R.vst3/` directory.
- Builds and packaging are automated via GitHub Actions.

## Installation

1. Unzip `MS2000R-v__VER__-win64.zip`.
2. Copy the `MS2000R.vst3` directory into your host's VST3 directory (e.g. `C:\Program Files\Common Files\VST3`).
3. Make sure the required ROM files and firmware are available (see the upstream project's README).
