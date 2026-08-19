# 🎯 GuruShots Auto Vote

**Automated GuruShots voting — desktop GUI, CLI, and Android, one shared engine.**

[![Platforms](https://img.shields.io/badge/platforms-macOS%20%7C%20Linux%20%7C%20Windows%20%7C%20Android-blue)](https://github.com/isthisgitlab/gurushots-auto-vote/releases)

> ⚠️ **Run only ONE instance at a time** — one GUI *or* one CLI *or* one phone. Multiple instances hammer the GuruShots API in parallel and can trigger rate-limits or account restrictions.

## ✨ Features

- **Automated voting** — votes your active challenges up to a configurable exposure target.
- **Last-minute push** — drives exposure to 100% inside a set window before a challenge closes, and polls more tightly as the deadline nears (with an optional lower ceiling for the final hour).
- **Boost & Turbo** — auto-applies boost near the deadline, and auto-plays the turbo mini-game to *earn* turbo, then *applies* it to a chosen entry before time runs out.
- **Auto-fill** — submits photos into empty entry slots near the deadline, staggered to avoid vote dilution, with tag and theme filters.
- **Per-challenge overrides** — every voting setting has a global default that any single challenge can override; tag rules key on the challenge *title* so they survive GuruShots' rotating challenge IDs.
- **Resilient** — configurable timeouts with automatic retry/backoff on transient API failures.
- **Quality of life** — light/dark themes, English/Latvian UI, timezone display, a mock mode for safe testing, and built-in update notifications.

## 🚀 Usage

**Most users:** grab a [release build](https://github.com/isthisgitlab/gurushots-auto-vote/releases) — the desktop GUI (macOS/Linux/Windows) or the Android APK — and run it.

**Command line** (`gurucli`, macOS & Linux):

```bash
./gurucli-<version>-<platform> login    # authenticate once (saves a token)
./gurucli-<version>-<platform> run      # one full auto-strategy cycle
./gurucli-<version>-<platform> start    # continuous voting (Ctrl+C to stop)
```

**From source** (pnpm 11+; `npm` is not supported):

```bash
pnpm install
pnpm start            # launch the desktop GUI
```

## 🏗️ Architecture

- **One shared engine** — all voting logic lives in `src/js/` and is reused across every platform; only the shell (entry point, transport, storage) differs.
- **Real / mock swap** — `apiFactory` selects the live GuruShots API or a mock at runtime based on the `mock` setting, so you can test safely.
- **Shared renderer** — a single Preact UI runs under both Electron (desktop) and Capacitor (Android).
- **Settings facade** — centralized configuration with a zod-validated schema and platform-specific storage.

## 📦 Platforms

| Platform    | GUI                        | CLI (`gurucli`)              |
|-------------|----------------------------|------------------------------|
| **macOS**   | `.dmg`                     | ✅ terminal binary            |
| **Linux**   | AppImage                   | ✅ x64 & ARM64                |
| **Windows** | Portable `.exe`            | — (use the GUI)              |
| **Android** | Sideloaded APK (votes in the background) | —              |

## 🔧 Tech Stack

- **Frontend**: Electron, Capacitor (Android), Preact + `@preact/signals`, TailwindCSS, DaisyUI
- **Core**: Node.js shared engine in `src/js/`, zod-validated settings
- **CLI**: `gurucli`, packaged as a Node Single Executable Application (SEA) via `postject`
- **Testing**: comprehensive Jest test suite
- **Build**: electron-builder (GUI) + Node SEA (CLI)

---

**[📥 Download Latest Release](https://github.com/isthisgitlab/gurushots-auto-vote/releases)** | **[📚 Full Documentation](https://github.com/isthisgitlab/gurushots-auto-vote)**
