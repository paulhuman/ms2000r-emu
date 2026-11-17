# Русский

Соглашения форка `paulhuman/ms2000r-emu`. Документ фиксирует правила версионирования, ветвления, публикации и оформления заметок к выпуску. Форк отслеживает upstream [`Tuth/ms2000r-emu`](https://github.com/Tuth/ms2000r-emu).

## Версионирование

### Формат тега

`v<base>-paulhuman.<n>`, где:

- `base` — версия upstream из `CMakeLists.txt`, строка `project(KorgMS2000 VERSION <base> ...)`;
- `n` — порядковый номер сборки форка на этой базе, начиная с 1.

Пример: `v0.9.10-paulhuman.1`. При переходе на новую версию upstream номер `n` начинается заново с 1.

### Строка версии в коде

`MS2K_VERSION` собирается как `<base><suffix>`, где суффикс передаётся при сборке:

```
-DMS2K_VERSION_SUFFIX=-paulhuman.1
```

В GitHub Actions суффикс вычисляется из тега автоматически. Строка видна в заголовке standalone-приложения и в окне плагина.

Числовое поле версии в метаданных VST3 берётся из `project(... VERSION)` и суффикс не содержит. Некоторые host показывают его в меню `About`; это ожидаемое поведение, менять его не требуется.

### Имя архива

`MS2000R-<tag>-win64.zip`, например `MS2000R-v0.9.10-paulhuman.1-win64.zip`. Архив распаковывается в готовый каталог `MS2000R.vst3/`.

## Ветки и публикация

- `main` — публикуемая ветка: изменения форка поверх upstream.
- Служебные ветки (например, `ms2000r-native/hooks` с отладочными инструментами emulator-хуков) не публикуются и в `main` не сливаются.
- Публикуется только `main` и теги на нём. Ветки с локальными экспериментами остаются локальными.

### Слияние новой версии upstream

```
git fetch upstream --tags
git switch main
git merge --no-edit v<base>
```

Конфликты разводятся вручную: изменения, которые upstream уже реализовал самостоятельно, заменяются его версией; изменения, которых у upstream нет, сохраняются. После сборки конфликтные функции сверяются с апстримным кодом.

## Заметки к выпуску

### Источник

Шаг `Create curated release notes` в `.github/workflows/release.yml` выбирает файл в таком порядке:

1. `release-notes/<tag>.md`, если файл существует — используется как есть;
2. `.github/workflows/release-notes.template.md` — заглушка с подстановками `__VER__`, `__BASE__`, `__DATE__` (ветка `workflow_dispatch` без тега).

Поэтому заметки пишутся заранее, до создания тега, и коммитятся в `main`.

### Формат файла

Двуязычный документ: русская часть, разделитель `---`, английская часть.

```
# Русский
...
---
# English
...
```

Разделы в каждой части, в этом порядке:

1. Вступление — одна строка: форк на основе upstream-версии `v<base>`.
2. Blockquote об ограничении сборки: только Windows (x64).
3. `**Upstream:**` — ссылка на тег upstream.
4. `## Изменения с версии <предыдущий тег>`; в первом выпуске на новой базе — `## Изменения относительно upstream v<base>`.
5. `### Для пользователей` — результат для обычного человека, без терминов реализации.
6. `### Для разработчиков` — затронутые файлы, флаги, механизмы.
7. `## Полный список изменений форка` — ссылка на каталог `release-notes/`.
8. `## Соглашения форка` — суффикс версии, формат VST3 bundle, автоматизация сборки.
9. `## Установка` — нумерованный список.

Английская часть повторяет структуру дословно (`## Changes since ...`, `### For users`, `### For developers` и так далее).

### Правила текста

- Русская часть пишется по правилам русской технической редакции: английские термины и официальные названия сохраняются в исходном написании, названия настроек и файлов оформляются в `inline code`.
- Пользовательский раздел описывает изменение поведения, а не устройство кода. Разработческий — файлы, флаги, механизмы.
- Изменения upstream и изменения форка разделяются явно; PR указываются только те, чьи изменения действительно входят в релиз.
- Неподтверждённые утверждения о производительности, стабильности и совместимости не включаются.

### Чеклист выпуска

1. Слить актуальную версию upstream в `main` (если она вышла).
2. Обновить `README.md`: заголовок версии и раздел `Selected changes in this fork`.
3. Написать `release-notes/<tag>.md`.
4. Собрать локально и прогнать `MS2000R_HostTest.exe state` — проверить сохранение состояния.
5. Закоммитить и запушить `main`.
6. Поставить тег и запушить его: `git tag <tag>` и `git push origin <tag>`.
7. Убедиться, что workflow прошёл, а в релизе верные заметки и архив.

## Непрерывная интеграция

- `.github/workflows/ci.yml` — сборка на `push` и `pull_request` в `main`, а также по `workflow_dispatch`; артефакт `vst3-win64-ci`.
- `.github/workflows/release.yml` — сборка и публикация релиза на тег `v*` и по `workflow_dispatch`.
- Релиз запускается только тегом с префиксом `v`. Тег без префикса workflow не активирует.
- Тест `MS2000R_HostTest.exe state` в CI не выполняется: для него нужны ROM-файлы и прошивки, которых нет в публичном репозитории. Проверка остаётся локальной.

---

# English

Conventions for the `paulhuman/ms2000r-emu` fork. This document records the rules for versioning, branching, publishing and release notes. The fork tracks upstream [`Tuth/ms2000r-emu`](https://github.com/Tuth/ms2000r-emu).

## Versioning

### Tag format

`v<base>-paulhuman.<n>`, where:

- `base` is the upstream version from `CMakeLists.txt`, the line `project(KorgMS2000 VERSION <base> ...)`;
- `n` is the fork build number on that base, starting at 1.

Example: `v0.9.10-paulhuman.1`. When the fork moves to a new upstream version, `n` restarts at 1.

### Version string in the code

`MS2K_VERSION` is built as `<base><suffix>`, with the suffix passed at configure time:

```
-DMS2K_VERSION_SUFFIX=-paulhuman.1
```

GitHub Actions derives the suffix from the tag automatically. The string shows up in the standalone window title and in the plugin's window.

The numeric VST3 version field comes from `project(... VERSION)` and carries no suffix. Some hosts show it in the `About` menu; that is expected and needs no change.

### Archive name

`MS2000R-<tag>-win64.zip`, for example `MS2000R-v0.9.10-paulhuman.1-win64.zip`. The archive unpacks into a ready `MS2000R.vst3/` directory.

## Branches and publishing

- `main` is the published branch: fork changes on top of upstream.
- Service branches (for example `ms2000r-native/hooks` with emulator debug hooks) are never published and never merged into `main`.
- Only `main` and its tags are published. Branches with local experiments stay local.

### Merging a new upstream version

```
git fetch upstream --tags
git switch main
git merge --no-edit v<base>
```

Resolve conflicts by hand: where upstream has implemented the same change itself, take its version; where it has not, keep ours. After a build, the conflicting functions are compared against the upstream code.

## Release notes

### Source

The `Create curated release notes` step in `.github/workflows/release.yml` picks a file in this order:

1. `release-notes/<tag>.md` when the file exists — used verbatim;
2. `.github/workflows/release-notes.template.md` — a placeholder with `__VER__`, `__BASE__`, `__DATE__` substitutions (the tagless `workflow_dispatch` path).

Notes are therefore written and committed to `main` before the tag is created.

### File format

A bilingual document: the Russian part, a `---` separator, the English part.

```
# Русский
...
---
# English
...
```

Sections in each part, in this order:

1. Intro — one line: the fork based on upstream `v<base>`.
2. A blockquote on the build limitation: Windows (x64) only.
3. `**Upstream:**` — a link to the upstream tag.
4. `## Changes since <previous tag>`; for the first release on a new base, `## Changes vs upstream v<base>`.
5. `### For users` — the outcome for a regular user, no implementation terms.
6. `### For developers` — affected files, flags, mechanisms.
7. `## Full list of fork changes` — a link to the `release-notes/` directory.
8. `## Fork conventions` — version suffix, VST3 bundle layout, build automation.
9. `## Installation` — a numbered list.

The Russian part mirrors the structure exactly (`## Изменения с версии ...`, `### Для пользователей`, `### Для разработчиков` and so on).

### Text rules

- The Russian part follows Russian technical writing conventions: English terms and official names keep their original spelling, setting and file names go into `inline code`.
- The user section describes a behaviour change, not the code. The developer section covers files, flags and mechanisms.
- Upstream changes and fork changes are kept apart; a PR is referenced only when its changes actually ship in the release.
- Unverified claims about performance, stability or compatibility are not included.

### Release checklist

1. Merge the current upstream version into `main` (if one was released).
2. Update `README.md`: the version in the title and the `Selected changes in this fork` section.
3. Write `release-notes/<tag>.md`.
4. Build locally and run `MS2000R_HostTest.exe state` to check state recall.
5. Commit and push `main`.
6. Create the tag and push it: `git tag <tag>` and `git push origin <tag>`.
7. Confirm the workflow passed and the release has the right notes and archive.

## Continuous integration

- `.github/workflows/ci.yml` — builds on `push` and `pull_request` to `main` and on `workflow_dispatch`; uploads the `vst3-win64-ci` artifact.
- `.github/workflows/release.yml` — builds and publishes a release on a `v*` tag and on `workflow_dispatch`.
- A release only starts from a tag with the `v` prefix. A tag without it does not trigger the workflow.
- `MS2000R_HostTest.exe state` does not run in CI: it needs ROM files and firmware that are not part of the public repository. The check stays local.