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
| **Android (Kotlin)** | v1.x | `MagicBattle-vX.Y.apk` — the original Kotlin app, versionCode 28 at v3.7; TalkBack + Prism speech; downloads and installs updates itself (resumable, digest-verified) |
| **Windows (C# / .NET 10)** | v3.3 | `MagicBattle-Windows-vX.Y.zip` — SDL3 graphics + SDL3_mixer sound, Prism speech; v3.7 ships as a **ReadyToRun AOT single-file** exe PLUS a true **NativeAOT** build produced by the repo's GitHub Actions workflow |

## Current release: v3.7

| Asset | Size | sha256 (GitHub API digest) |
|---|---|---|
| `MagicBattle-v3.7.apk` | 15.4 MB | `f6f52073406278c8b6de7b28aec9bb67c1498560778c1ddc19572676eb5f4b46` |
| `MagicBattle-Windows-v3.7.zip` | 20.8 MB | `a87caf7b2d157dd7bfa4d65d4e76854515d283b59b546118ea258c60430d6d22` |
| `MagicBattle-Windows-NativeAOT-v3.7.zip` | 13.1 MB | `976276aa719bd8ae3a4d67c5c0114ecd162c8476ab4a6726001f2638bc31f5af` |

**v3.7 highlights**

- **Admin management stored in the accounts DB** (`users.is_admin`) — admins survive restarts and the DB stays 100% python-compatible; the **first account ever registered is automatically an admin**.
- **Add / remove admin** — the control panel (F11 on Windows, Control Panel on Android) gets an **Admins** section: pick an admin -> remove. Every promote / demote **kicks the target once** with the reason ("You are now an admin." / "You are no longer an admin.") and the **kick sound** — so they know it took effect.
- **Temporary bans (minutes)** — same hardware-fingerprint coverage as a full ban, but it **expires on its own**; enter any number of minutes (up to 2 days) and the **ban list shows the time left** (permanent bans are marked). Expired bans disappear without any admin action.
- **Staff sounds** — the kicked player hears `kick.ogg`; the banned player hears `ban.ogg` (again when their login/register is denied); when anyone is **unbanned, EVERY player present on the server hears `unban.ogg`** plus an announcement of who came back.
- Server CLI stays simple: `MagicBattle.Server 7777` (positional port) or just `MagicBattle.Server` (default 7777); `MB_DB_PATH` env var picks the accounts DB.

**Windows variants**: `MagicBattle-Windows-v3.7.zip` = ReadyToRun single-file `MagicBattle.exe` (recommended; keep the SDL3/SDL3_mixer/codec DLLs and `prism.dll` next to it, `sounds/` is a plain folder — now including kick/ban/unban). `MagicBattle-Windows-NativeAOT-v3.7.zip` = the same game fully **NativeAOT**-compiled by the GitHub Actions `windows-native-aot` workflow on a Windows runner — same layout, smaller exe, no IL at all.

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
