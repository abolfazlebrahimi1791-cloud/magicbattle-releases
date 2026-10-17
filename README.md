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
| **Android (Kotlin)** | v1.x | `MagicBattle-vX.Y.apk` — the original Kotlin app, versionCode 29 at v3.8; TalkBack + Prism speech; downloads and installs updates itself (resumable, digest-verified) |
| **Windows (C# / .NET 10)** | v3.3 | `MagicBattle-Windows-vX.Y.zip` — SDL3 graphics + SDL3_mixer sound, Prism speech; v3.8 ships as a **ReadyToRun AOT single-file** exe PLUS a true **NativeAOT** build produced by the repo's GitHub Actions workflow |

## Current release: v3.8

| Asset | Size | sha256 (GitHub API digest) |
|---|---|---|
| `MagicBattle-v3.8.apk` | 15.4 MB | `86981312d9addc6957ff2e4d90701ba7343bc87a69ccdc31948ac3eb18e4d717` |
| `MagicBattle-Windows-v3.8.zip` | 16.5 MB | `e0113fdded1593406b73ad5a74b223ad7c1a56d78ac0741a93f32edf8568a3b0` |
| `MagicBattle-Windows-NativeAOT-v3.8.zip` | 13.1 MB | `2155b5928aec4332aa500aec9fe911e77c6905f4d206ac9e46dbaf1afb355db8` |

**v3.8 highlights**

- **Per-user global chat mute** — the admin can turn ONE user's **global chat OFF** (the "swearing user" switch): control panel -> pick a player -> **Turn global chat OFF**. The flag lives in the accounts DB (`users.chat_muted`), so it survives restarts and reconnects.
- The muted player is **told the moment it flips** ("An admin turned your global chat off." / "... back on."), and every global message they send is **blocked** with "Your global chat is disabled by an admin." — **table (local) chat and the game itself stay free**.
- The panel marks muted players with **(chat off)** and offers the matching action (mute when open, unmute when muted) — on both the Android panel (menu -> Control Panel, also inside the table via **More options**) and the Windows **F11** panel.
- Everything from v3.7 stays: **add / remove admin** (each with the ONE confirmation kick + kick sound), **temporary bans in minutes** with self-expiry and countdown in the ban list, **hardware-fingerprint bans** ("you are banned" on login AND register — a banned device cannot even create a new account), the **auto-admin first account**, the **unban sound heard by EVERYONE** on the server, and the simple server CLI (`MagicBattle.Server 7777`, `MB_DB_PATH` env var).

**Windows variants**: `MagicBattle-Windows-v3.8.zip` = ReadyToRun single-file `MagicBattle.exe` (recommended; keep the SDL3/SDL3_mixer/codec DLLs and `prism.dll` next to it, `sounds/` is a plain folder). `MagicBattle-Windows-NativeAOT-v3.8.zip` = the same game fully **NativeAOT**-compiled by the GitHub Actions `windows-native-aot` workflow on a Windows runner — same layout, smaller exe, no IL at all.

## Install

### Android
1. Download `MagicBattle-v3.7.apk` from the latest release (or let the installed app do it — it speaks the changelog, verifies the sha256 digest and resumes broken downloads).
2. Allow "install unknown apps" for the source app if asked.
3. Install — it updates the existing game in place.

### Windows
1. Download one of the two v3.7 Windows zips and unzip it anywhere.
2. Run `MagicBattle.exe`. Keep the DLLs and the `sounds/` folder next to it.

## Older releases

Older tags (v1.x – v3.6) stay available in the Releases list. Since v3.3 the Windows client is the C# port; the v3.3/v3.4 Android APKs were the experimental C# build (versionCode 23/24) — since v3.5 the Android client is the original Kotlin app (versionCode 28 now), which is the recommended client.
