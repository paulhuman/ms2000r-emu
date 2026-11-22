# AGENTS.md

Rules for agents and contributors working in this repository. Read them before
committing, tagging or publishing anything.

## Repository

This is a public fork of [`Tuth/ms2000r-emu`](https://github.com/Tuth/ms2000r-emu).

- `main` is the only published branch. It carries the fork's changes on top of upstream.
- Service branches (for example `ms2000r-native/hooks`, which holds emulator debug
  hooks) are never pushed and never merged into `main`.
- `origin` is this fork, `upstream` is `Tuth/ms2000r-emu`.
- Versioning, release notes and the release checklist are described in
  [docs/fork-conventions.md](docs/fork-conventions.md).

## Commit messages

**Write commit messages in English.** The whole history is English, both upstream
and the fork's own commits; a Russian message breaks that.

- Use Conventional Commits: `type(scope): description`.
- Types in use: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`,
  `build`, `ci`, `chore`.
- The description starts with a lowercase word and has no trailing period.
- The body explains what changed and why, wrapped at 100 characters.
- No `Co-authored-by` or AI-attribution trailers unless asked for.

## Release notes

- Release notes are written **before** the tag and committed to `main` as
  `release-notes/<tag>.md`.
- They are bilingual: Russian first, then `---`, then English.
- Russian text follows Russian technical writing conventions: English technical
  terms and official names keep their spelling, setting and file names use
  inline code.
- Keep the user-facing sections free of maintainer material: repository rules,
  file paths of internal docs and similar pointers belong in the docs, not in a
  release description.
- A PR is credited only when its changes actually ship in that release.

## Code and documentation language

- Source code, comments, `README.md` and repository documentation are English.
- `docs/fork-conventions.md` and release notes are bilingual (Russian and English).
- The notice at the top of `README.md` is bilingual (Russian and English).

## Build

- Windows: MSVC with CMake. The CI builds on `windows-latest` with the default
  generator; locally the project is normally built with Ninja.
- `cmake --build build --target MS2000R_Shim` produces the VST3 bundle in
  `build/VST3_multi/MS2000R.vst3`.
- `MS2000R_HostTest.exe state` needs the ROM files and firmware; it stays a local
  check because neither is part of this public repository.

## Before pushing

1. Build the shim and, when the change can affect recall, run the state round-trip.
2. Check `git status` — no stray files, no conflict markers.
3. Push `main` only, then create the tag and push it separately.