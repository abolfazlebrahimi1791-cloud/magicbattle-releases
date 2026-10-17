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
| **Android (Kotlin)** | v1.x | `MagicBattle-vX.Y.apk` — the original Kotlin app, versionCode 27 at v3.6; TalkBack + Prism speech; downloads and installs updates itself (resumable, digest-verified) |
| **Windows (C# / .NET 10)** | v3.3 | `MagicBattle-Windows-vX.Y.zip` — SDL3 graphics + SDL3_mixer sound, Prism speech; v3.6 ships as a **ReadyToRun AOT single-file** exe PLUS a true **NativeAOT** build produced by the repo's GitHub Actions workflow |

## Current release: v3.6

| Asset | Size | sha256 (GitHub API digest) |
|---|---|---|
| `MagicBattle-v3.6.apk` | 14.1 MB | `54e1f6ce352f0c3f76527cd7c2dfd9a88845f81c85bf099dc01646e177bd8cf0` |
| `MagicBattle-Windows-v3.6.zip` | 20.7 MB | `b6c23f295a9ad1f05006e960714a93593cdb715defeb2e3786ee1f215d47747d` |
| `MagicBattle-Windows-NativeAOT-v3.6.zip` | 12.9 MB | `11313263472db2b165a1c51beb2f364e2a266ca8d8cf80f88b2528da9dece3c3` |

**v3.6 highlights**

- **Staff control panel** (admins): Windows **F11** (lobby + tables), Android **Control Panel** in the online menu and the in-table "more options" — online players with a **search**, then Kick / Ban / Make admin; the banned list with Unban.
- **Hardware-fingerprint bans** — a stable device id (Windows: MachineGuid/CPU/board/volume serial/RAM; Android: ANDROID_ID/build constants/RAM/storage/screen) is sent with login/register; a banned device cannot even create an account: it gets exactly **"you are banned"**.
- **First account auto-admin** — register once on a fresh server and your account administers everyone.
- **"X (admin) is online"** — announced instantly to everyone when an admin logs in.
- **Local/global chat** — `/text` = this table, `\text` = everyone; on Android: two buttons, **Send local** / **Send global**.
- The server (private `v3.6-server` release) runs the simple way: `MagicBattle.Server 7777` or just `MagicBattle.Server` (default 7777) — never a service.

**Windows variants**: `MagicBattle-Windows-v3.6.zip` = ReadyToRun single-file `MagicBattle.exe` (recommended; keep the SDL3/SDL3_mixer/codec DLLs and `prism.dll` next to it, `sounds/` is a plain folder). `MagicBattle-Windows-NativeAOT-v3.6.zip` = the same game fully **NativeAOT**-compiled by the GitHub Actions `windows-native-aot` workflow on a Windows runner — same layout, smaller exe, no IL at all.

## Install

### Android
1. Download `MagicBattle-v3.6.apk` from the latest release (or let the installed app do it — it speaks the changelog, verifies the sha256 digest and resumes broken downloads).
2. Allow "install unknown apps" for the source app if asked.
3. Install — it updates the existing game in place.

### Windows
1. Download one of the two v3.6 Windows zips and unzip it anywhere.
2. Run `MagicBattle.exe`. Keep the DLLs and the `sounds/` folder next to it.

## Older releases

Older tags (v1.x – v3.5) stay available in the Releases list. Since v3.3 the Windows client is the C# port; the v3.3/v3.4 Android APKs were the experimental C# build (versionCode 23/24) — since v3.5 the Android client is the original Kotlin app (versionCode 27 now), which is the recommended client.
