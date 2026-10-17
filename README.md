# Magic Battle — Releases

This repository hosts the **public release downloads** of the Magic Battle game: the Android APK and the Windows client.

- The **source code lives in a private repository** — it is not published here.
- The clients check this repo's Releases through the public GitHub API (no account, no token, no tracking).
- Android only installs an update signed with the app's own key, so only APKs published here (and signed by the developer) can update the installed app.

## How updates are verified

Since v3.3 every asset is verified with the **sha256 digest that the GitHub REST API itself returns** (`assets[].digest`). No `.md5` sidecar files are published anymore — the API response is the single source of truth, and a download that does not match the digest is deleted automatically before the install button is ever offered.

## Clients

| Client | Since | Notes |
|---|---|---|
| **Android (Kotlin)** | v1.x | `MagicBattle-vX.Y.apk` — the original Kotlin app, versionCode 26 at v3.5; TalkBack + Prism speech; downloads and installs updates itself (resumable, digest-verified) |
| **Windows (C# / .NET 10)** | v3.3 | `MagicBattle-Windows-vX.Y.zip` — SDL3 graphics + SDL3_mixer sound, Prism speech; v3.5 ships as a **ReadyToRun AOT single-file** exe; Windows only *announces* the download link, it never downloads in place |

## Current release: v3.5

| Asset | Size | sha256 (GitHub API digest) |
|---|---|---|
| `MagicBattle-v3.5.apk` | 14.1 MB | `8cc678a8530b810e301f2f1cf17e5b54d7e4f0a57bed71c3aa0196c5562bea68` |
| `MagicBattle-Windows-v3.5.zip` | 20.7 MB | `989dc2c40d8d2af6482348623cd5d93dc24c699fbf0fb3c5ea68fc9381909e30` |

- **v3.5 Android = Kotlin again** (versionCode 26 / versionName 3.5) — the gradle build with the spectator protocol fix (`spectator` instead of `on`), the slimmer updater and the screen reworks that had not shipped yet. Installs over every previous build (Kotlin 22, C# 23/24/25) — same signing key.
- **v3.5 Windows = ReadyToRun AOT** — self-contained trimmed single-file `MagicBattle.exe` with native R2R code baked in at publish time (faster startup). The SDL3/SDL3_mixer/codec DLLs and `prism.dll` must stay next to the exe; `sounds/` is a plain folder like before.
- True **NativeAOT** Windows builds are produced by the source repo's `windows-native-aot` GitHub Actions workflow (a windows-x64 NativeAOT binary can only be built on Windows itself — .NET does not support cross-OS NativeAOT).
- The **server is not published here** — it is C# / .NET 10 and ships only in the private source repo (`v3.5-server` release: linux-x64 NativeAOT binary + win-x64 self-contained), same WebSocket protocol and a 100% compatible `accounts.db`.

## Install

### Android
1. Download `MagicBattle-v3.5.apk` from the latest release (or let the installed app do it — it speaks the changelog, verifies the sha256 digest and resumes broken downloads).
2. Allow "install unknown apps" for the source app if asked.
3. Install — it updates the existing game in place.

### Windows
1. Download `MagicBattle-Windows-v3.5.zip` and unzip it anywhere.
2. Run `MagicBattle.exe`. Keep the DLLs and the `sounds/` folder next to it.

## Older releases

Older tags (v1.x – v3.4) stay available in the Releases list. Since v3.3 the Windows client is the C# port; the v3.3/v3.4 Android APKs were the experimental C# build (versionCode 23/24) — v3.5 returns to the original Kotlin app (versionCode 26), which is the recommended client.
