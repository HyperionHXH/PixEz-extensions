# PixEz-extensions

Standalone PixEz extension repository for Mihon and Suwayomi.

## Mihon repository

Current Mihon versions use:

```text
https://raw.githubusercontent.com/HyperionHXH/PixEz-extensions/repo/index.json
```

Older Mihon/Suwayomi builds can use:

```text
https://raw.githubusercontent.com/HyperionHXH/PixEz-extensions/repo/index.min.json
```

The `main` branch contains the PixEz source and required build infrastructure. The `repo` branch contains published metadata and artifacts. APKs keep the same signing key between releases so Mihon can update an installed extension. The included GitHub Actions workflow separates the signing build from the repository-writing publish job.

## PixEz features

PixEz is a separate extension package (`eu.kanade.tachiyomi.extension.all.pixez`), so it can be installed alongside the older Pixiv extension. It supports anonymous ranking/latest/search browsing and, after login, recommended feeds, public/private following, public/private bookmarks, bookmark-tag lists, user works, related works, series watchlist, multi-page reading, and bookmark/follow/watchlist actions.

The extension settings accept a Pixiv refresh token. The extension exchanges it for a short-lived access token locally and refreshes it when needed; no account, password, cookie, or token is committed to this repository. Use **Verify login** after entering the token. The local test APK is `PixEz-v1.6.3.apk` in the repository root; CI-built releases use the repository signing key.

For Mihon/Suwayomi, add the repository URL above, install **PixEz**, and configure the token in the source settings. Private feeds and bookmark tags cannot be tested without a valid token and an account permitted to access them.

Every push and pull request runs a tracked-file credential scan. Signing material is supplied only through GitHub Actions secrets and is never committed to either branch.

## Build

```powershell
C:\Temp\gradle-9.7.0\bin\gradle.bat :src:all:pixez:assembleRelease :src:all:pixez:lintRelease --no-daemon
```

Artifacts are written under `src/all/pixez/build/outputs/apk/release` and `src/all/pixez/build/outputs/jar/release`.
