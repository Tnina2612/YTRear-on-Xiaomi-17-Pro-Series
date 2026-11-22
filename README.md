# YTRear

**English** · [Tiếng Việt](README.vi.md)

[![Latest release](https://img.shields.io/github/v/release/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series?style=flat-square&label=release)](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/releases)
[![CI](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/actions/workflows/ci.yml)
[![Release workflow](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/actions/workflows/release.yml/badge.svg?branch=main)](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/actions/workflows/release.yml)
[![License](https://img.shields.io/github/license/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series?style=flat-square)](LICENSE)
[![Downloads](https://img.shields.io/github/downloads/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/total?style=flat-square)](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/releases)
[![Platform](https://img.shields.io/badge/platform-Android%2016%20%2F%20HyperOS-3ddc84?style=flat-square&logo=android&logoColor=white)](#install)

> **Maintained fork.** This repository is a fork of
> [megadonkatsu/YTRear](https://github.com/megadonkatsu/YTRear) with fixes and features added on
> top. The original repository is no longer maintained: its owner is inactive and does not respond
> to issues or pull requests. Please report bugs and open pull requests in
> [this fork](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series) instead of upstream.

The fork keeps the original rear-screen proxying approach and adds several practical improvements:

- **Automatic player following** with per-app exclusions, so the rear card moves between players
  without reopening YTRear.
- **A fuller setup flow**: battery-optimization onboarding, a Quick Settings on/off tile, and a
  single checklist for notification access, battery, and HyperOS autostart.
- **Firmware verification** for both HyperOS `OS3.0.318.0.WBLCNXM` and `OS4.0.6.0.XBLCNXM`, with a
  warning instead of silently assuming an untested rear-screen path.
- **Vietnamese localization** with an in-app language picker, while English remains the base locale.
- **A cleaner permission story**: the full HyperOS-native player allowlist is excluded and the
  obsolete overlay permission and probes are gone.

Control a selected Android music player from the Xiaomi 17 Pro rear "Magic Back Screen" while the
main display is off. Runs on a locked, non-rooted phone — no Shizuku, no privileged install.

Latest public release: **1.5.1** (`versionCode 19`) — auto-detect the most recently active player or
pick any specific app, with a consolidated setup checklist, firmware verification, and Vietnamese
localization. See the [changelog](CHANGELOG.md) for what changed, and
[releases](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/releases) for the signed APK.
Version 1.2 remains the tagged stable baseline.

## What's new in 1.5.1

- **A single Setup card** replaces the separate notification-access and battery buttons. It shows
  notification access, battery exemption, and HyperOS autostart together, and hides once all three
  are complete.
- **Autostart confirmation.** HyperOS does not expose the autostart state to apps, so YTRear opens
  the system screen and records your confirmation with a checkbox. The card also reminds you to keep
  YTRear in Recents, since swiping it away is treated as a force-stop.
- **Firmware verification.** Validated HyperOS builds now include both `OS3.0.318.0.WBLCNXM` and
  `OS4.0.6.0.XBLCNXM`. An unverified build shows a quiet warning inside **Advanced** and reports its
  status in diagnostics.
- **Vietnamese UI and language picker.** The globe button at the top-right switches between
  **Theo hệ thống**, **English**, and **Tiếng Việt**. The choice is stored per app, survives
  restarts, and also localizes the foreground-service and media notifications.

## What's new in 1.5.0

- **Battery setup is now part of onboarding.** The main screen keeps a **Set battery to No
  restrictions** button visible until YTRear is exempt from battery optimization, so HyperOS's
  Greezer cannot freeze the process five seconds after you leave the app or turn the screen off. The
  diagnostics panel reports the current state. The 1.5.1 Setup card replaces this standalone button.
- **Quick Settings tile.** Add YTRear to the shade to turn the rear-screen proxy on or off with one
  tap, without opening the app. Turning it off clears the proxy and returns your selected player's
  own media notification; turning it on restores both. The tile is only active once notification
  access is granted and a player is configured, and a tap during setup opens YTRear.
- **Icons in the player picker.** The picker now shows each app's launcher icon and keeps the
  auto-detect row pinned first, loading icons off the main thread so scrolling stays smooth.

## What's new in 1.4.1

- **Full HyperOS native-player allowlist exclusion.** Every music app that HyperOS already supports
  natively on the rear screen (`Spotify`, `Xiaomi Music`, `QQ Music`, `NetEase Cloud Music`,
  `Kugou`, and `Kuwo`) is now skipped by both the manual picker and auto-detection so the firmware's
  native widget handles them directly.
- **No overlay permission required.** Removed `SYSTEM_ALERT_WINDOW` and the obsolete early-research
  overlay/custom-widget probes. YTRear now requests only notification and foreground-service
  permissions.
- **Automated CI.** Added GitHub Actions CI to verify `:app:assembleDebug` and `:app:lintDebug` on
  every push and pull request.

## What's new in 1.4.0

- **Auto-detect active player.** Choose **Auto-detect active player** at the top of the player
  picker to let YTRear follow whichever eligible music app most recently started playing, without
  reopening YTRear to switch targets. Manual single-player selection remains available at any time.
- **Stationary rear-card handoffs.** When a new player takes audio focus, YTRear primes HyperOS's
  `< 200 ms` rear-widget retention window, switches the proxy session in place, snoozes the new
  player's `MediaStyle` notification, and releases the previous player's notification back to the
  shade.
- **Per-app exclusions.** In auto mode, **Excluded apps** on the main screen opens a searchable
  checklist of launchable apps that auto-detect should ignore so video or browser apps can keep
  their own media cards.
- **Verified on-device across live multi-player handoffs** (`YT Music Morphe` ↔ `SoundCloud`) with
  zero rear-widget removals, immediate notification restoration, and full transport forwarding.

## What's new in 1.3.2

- **Switching players now cleans up after itself.** When you pick a different player, YTRear
  releases the previous one's snoozed media notification instead of leaving it suppressed for the
  rest of its 30-day timer. Android gives ordinary notification listeners no way to unsnooze
  directly, so YTRear shortens the existing snooze to 250 ms and lets Android repost the
  notification normally — after the new target has already taken over.
- **The cleanup survives restarts.** Pending restorations are persisted, so a switch still resolves
  correctly even if the notification listener is disconnected or the process is restarted at the
  time.
- **Verified on-device in both directions.** Switching away from actively playing YouTube Music
  cleared it from both Android snooze lists and restored its native notification immediately;
  switching back re-snoozed only YouTube Music. If the previous player isn't running, its
  notification returns the next time it posts one.

## What's new in 1.3.1

- **Pick any player.** A searchable picker opens with the main screen and lists every installed app
  that has a launcher. Choose the one YTRear should mirror; the choice persists across restarts and
  reboots, and **Player** on the main screen switches it at any time.
- **The Dynamic Island fix now follows your selection.** The notification workaround validated for
  YouTube Music in 1.2 applies to whichever player you select: YTRear snoozes that app's own
  MediaStyle notification and posts its proxy in its place, so the original card cannot retake
  HyperOS's top-media rank and collapse the expanded Dynamic Island during Next or Previous.
- **Applied the moment it matters** — when you switch players, when the notification listener
  connects, and whenever the selected player posts a new media notification.
- **Verified on-device with Poweramp** alongside the full YouTube Music regression. Spotify is
  omitted from the picker because this firmware already drives it natively.

## How it works

HyperOS gates its native rear music widget on an exact package-name allowlist. It does not check
the certificate, installer, UID lineage, or privileged status at that gate. YTRear builds under
an allowlisted package identity, mirrors the selected app's `MediaSession` through a notification-
listener-authorized `MediaController`, and republishes it to the native rear widget. Transport
callbacks from the rear screen are forwarded back to that app.

```text
Selected player's MediaSession
        |  MediaController (notification listener)
        v
    MediaHub.kt
        |  metadata, artwork, playback state, position
        v
 NativeMediaProxy.kt
        |
        v
 HyperOS unified.music:music_media rear widget
        |  native MediaSession callbacks
        +---> selected player's transport controls
```

## Install

Download the APK from the [latest release](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/releases) and
sideload it — copy it to the phone and tap it, or `adb install -r YTRear-1.5.1-debug.apk`. HyperOS
will ask you to allow installs from whichever app you opened it with. Each release ships a
`.sha256` file; check it against your download before installing.

Then set these up, all on YTRear:

| Setting | Where | Why |
|---|---|---|
| **Notification access** | Settings → Apps → Special app access → Notification access | Required. This is how YTRear reads the selected player's media session. Nothing works without it. |
| **Notifications** | The prompt on first launch | YTRear's rear-screen card *is* a notification. Denying this breaks the widget. |
| **Autostart** | Setup card → **Open**, then tick **Autostart is enabled** | Lets the listener rebind after a reboot or a restart of the selected player. |
| **Battery saver: No restrictions** | Setup card → **Set** (or HyperOS app info → Battery saver) | Stops HyperOS freezing the proxy while the screen is off. The row turns green when the exemption is granted. |

Open YTRear and choose how to select a player. Pick **Auto-detect active player** at the top of the
list to follow whichever music app starts playing, or select one specific app to mirror. Grant the
requested access, then open your player and start playback. The **Setup** card hides automatically
once notification access, battery exemption, and autostart are all confirmed.

YTRear follows the system language by default. Use the globe button at the top-right of the main
screen to switch between **Theo hệ thống** (system default), **English**, and **Tiếng Việt** at any
time.

### Daily use

In **Auto-detect** mode, YTRear remembers the mode and the last active player across restarts and
reboots; starting playback in another eligible player switches the rear card automatically, and
**Excluded apps** lets you ignore specific apps. In **Manual** mode, YTRear asks for the target
whenever its main screen is opened and remembers the current selection. Use **Player** on the main
screen to change modes or targets at any time. For a quicker toggle, add **YTRear** to the Quick
Settings shade: one tap turns the proxy off and hands your player's own media notification back, and
another tap turns it on again.

Don't swipe YTRear away from Recents. HyperOS treats that as a force-stop and will refuse to rebind
the notification listener until you reopen the app.

## Player compatibility

The selected app must publish a standard Android `MediaSession`. Play/pause, next, previous,
metadata, and artwork depend on what that session exposes. Apps without a media session can still
be selected, but YTRear will remain at **Waiting for music**.

Apps in HyperOS's compiled rear-music allowlist (such as Spotify, Xiaomi Music, QQ Music, NetEase
Cloud Music, Kugou, and Kuwo) are intentionally omitted from both the picker and auto-detection
because this Xiaomi firmware already supports them on the rear screen without a proxy.

The selected player's MediaStyle notification is snoozed while YTRear supplies the replacement
player. This prevents the original app from taking back HyperOS's top-media rank and collapsing the
expanded Dynamic Island during a skip. YouTube Music is the fully validated target; Poweramp's
session, controls, and notification replacement have been verified on-device. Other apps that
expose a standard MediaSession should work but still need physical regression testing.

### Selected-player notification note

No permission or setting changes are needed on the selected player itself. One thing to leave
alone:

**Keep the selected player's notifications enabled.** Don't turn them off app-wide. YTRear works
*with* its media notification — it snoozes that notification and posts its own in its place.

Expect the selected player's media notification to vanish from the shade while YTRear is running.
That is deliberate, not a fault: if both appear in SystemUI, HyperOS drops YTRear's Dynamic Island
entry during a skip. Playback is untouched, and YTRear's card becomes the visible player. To get
the native notification back, tap YTRear's Quick Settings tile off (or disable YTRear's notification
access), then force-stop and reopen the player.

When another player is selected, YTRear automatically releases the previous player's snoozed
notification. If that player is still running, its notification can return immediately; otherwise,
it appears normally the next time the player starts or posts a media notification.

Uninstalling YTRear does not change the selected player's settings or data. Android may retain the
currently snoozed notification after uninstall; if it does not return immediately, force-stop the
player, reopen it, and start playback.

## Build

Requires JDK 17 and the Android SDK (compileSdk 36, build tools 36.0.0).

```bash
./gradlew :app:assembleDebug
```

The APK lands at `app/build/outputs/apk/debug/app-debug.apk`.

The 1.5.1 release APK is also archived locally at `releases/YTRear-1.5.1-debug.apk` with SHA-256
`1F7AE9113AE52F118469ED1DD7DEBD07804B64BEC97312E956BB086A100A395B`. It reports
`com.luna.music` version 1.5.1 (`versionCode 19`) and upgrades over 1.5.0 while keeping app data and
permissions.

### Releasing

The **Release** workflow runs on every push to `main`. It reads `versionName` and `versionCode` from
`app/build.gradle.kts`, builds the debug APK, creates the `v<version>` tag when it does not exist,
and publishes a GitHub Release with the APK and its `.sha256`. If that release already exists, the
workflow exits without rebuilding. If the tag exists on a different commit, it stops with an error
instead of moving the tag.

Run it manually from **Actions** → **Release** → **Run workflow** after a version bump. If a stale
tag from an earlier attempt exists, delete it first with `git tag -d vX.Y.Z` and
`git push origin :refs/tags/vX.Y.Z`.

## Package identity

The build sets `applicationId` to a package name that is on the firmware's rear-music map, while
the Kotlin namespace stays `dev.ytrear.app`. Android cannot install the genuine owner of that
package alongside this build. Use it only on a device you own, for interoperability testing.

## Issues and contributions

The upstream repository is inactive. Report bugs, request features, and send pull requests in
[this fork's issue tracker](https://github.com/Tnina2612/YTRear-on-Xiaomi-17-Pro-Series/issues).
If the Issues tab is unavailable, leave a comment on the latest release.

If YTRear is useful, a star on the repository is appreciated.

## License

The fork's original changes are released under the [MIT License](LICENSE). The upstream project did
not include a license file, so upstream code remains subject to its original author's rights; see
[NOTICE](NOTICE) for details.

## Docs

- [Changelog](CHANGELOG.md) — versioned behavior changes and removal notes
- [Research](docs/RESEARCH.md) — reverse-engineering findings and rejected approaches
- [Testing](docs/TESTING.md) — validation status and diagnostic commands
- [Version and rollback](docs/ROLLBACK.md) — pinned 1.2 baseline and tested downgrade commands

Tested against Android 16 / SDK 36 on a Xiaomi 17 Pro with HyperOS `OS3.0.318.0.WBLCNXM` and
`OS4.0.6.0.XBLCNXM`. The rear widget path is firmware-specific; builds outside that verified list
show a warning in **Advanced** instead of assuming identical behavior.
