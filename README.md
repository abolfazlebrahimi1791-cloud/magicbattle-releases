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
| **Android (Kotlin)** | v1.x | `MagicBattle-vX.Y.apk` — the original Kotlin app, versionCode 30 at v3.9; TalkBack + Prism speech; downloads and installs updates itself (resumable, digest-verified) |
| **Windows (C# / .NET 10)** | v3.3 | `MagicBattle-Windows-NativeAOT-vX.Y.zip` — SDL3 graphics + SDL3_mixer sound, Prism speech; **NativeAOT single-file exe** built by the repo's GitHub Actions workflow (AOT-only since v3.9) |

## Current release: v3.9

| Asset | Size | sha256 (GitHub API digest) |
|---|---|---|
| `MagicBattle-v3.9.apk` | 15.4 MB | `666292cbfd91813d9385d834384a5bc12fee66eee6131c0820fcf9bbe43f0992` |
| `MagicBattle-Windows-NativeAOT-v3.9.zip` | 13.3 MB | `4ed47bd4528c8e78c9f51e0cb0b92d7ffcf9562104b9eb4ebdba6e9b386651e8` |

### Highlights of v3.9

- The **offline packet** on every disconnect + a graceful logout ("X left
  the game") — no more ghost presences.
- A **ban anchors on EVERY hardware fingerprint** the account has ever
  used — each device banned separately, no escape.
- **Admin panel**: Add admin (search + accounts list) / Remove admin
  (live search) / Online players / Banned / **Delete account** (confirm,
  full DB removal).
- **Kick returns to the main game menu** on both clients; Android chat
  close returns to the exact screen (session stays alive).
- **Windows**: first-letter menu navigation, no cut speech, chat echo
  (F2 letters/words/off), caret reading with Left/Right ("blank" at the
  end) and a real **updater** (download/extract/replace/close).
- **AOT-only builds**: Windows NativeAOT from GitHub Actions + Linux
  NativeAOT server (private `v3.9-server` release in the source repo).
