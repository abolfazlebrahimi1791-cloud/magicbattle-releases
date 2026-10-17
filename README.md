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
| Android (`MagicBattle-vX.Y.apk`) | v2.x | native accessible UI, Prism speech, in-app updater |
| Windows (`MagicBattle-Windows-vX.Y.zip`) | v3.3 | SDL3 graphics + SDL3_mixer sound, Prism (SAPI) speech, the update check announces the download link only — it never auto-downloads |

## Install / Update

### Android

1. Download the newest `MagicBattle-vX.Y.apk` from [Releases](https://github.com/abolfazlebrahimi1791-cloud/magicbattle-releases/releases), **or**
2. simply start the app — the spoken "Checking for updates..." page runs first and offers the download + install automatically when a newer release exists (v2.14+).

### Windows

1. Download the newest `MagicBattle-Windows-vX.Y.zip` from [Releases](https://github.com/abolfazlebrahimi1791-cloud/magicbattle-releases/releases).
2. Unzip anywhere and run `MagicBattle.exe`.
3. When a new version is released, the client announces the version and the direct download link (in speech + message history).

## Latest release

- **v3.3** — first C# / .NET 10 release: Android client (versionCode 24, installs over 3.2 and earlier 3.3 builds; the 31 game sounds now ship as plain APK assets) + the first Windows client. Updater hash now comes from the GitHub API (sha256).
