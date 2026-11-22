# Changelog

## 1.5.1 - 2026-11-18

- Added a **Setup** checklist that combines notification access, battery exemption, and HyperOS
  autostart in one card. Rows show their current state, link to the relevant system screen, and the
  card hides once all three are complete.
- HyperOS does not expose its autostart state to apps, so YTRear now records a user confirmation
  (`Setup.kt`) after opening the autostart screen. A local note reminds users to keep YTRear in
  Recents, because swiping it away is treated as a force-stop.
- Added firmware verification for `OS3.0.318.0.WBLCNXM` and `OS4.0.6.0.XBLCNXM` (`Firmware.kt`).
  Unverified builds show a warning in **Advanced**, and diagnostics report the running build and
  support state.
- Added complete **Vietnamese localization** and a top-right language button with **Theo hệ thống**,
  **English**, and **Tiếng Việt** choices. The app uses AppCompat per-app locales with
  `android:localeConfig` plus `autoStoreLocales` for API < 33, and the choice persists across
  restarts.
- Localized the foreground-service channel/title/body, the proxy notification channel, and the
  media notification actions.
- Added English and Vietnamese READMEs with release/CI/license badges, plus an MIT license for the
  fork's original changes and a NOTICE covering the unlicensed upstream project.
- Added a **Release** GitHub Actions workflow that reads the Gradle version, builds the debug APK,
  creates the matching `v<version>` tag, and publishes the GitHub Release with the APK and
  `.sha256`.
- Bumped the release to version 1.5.1 (`versionCode 19`). Upgrading from 1.5.0 keeps app data,
  notification access, and the saved player selection.

## 1.5.0 - 2026-11-17

- Added a battery setup prompt: the main screen checks
  `PowerManager.isIgnoringBatteryOptimizations()` and keeps a **Set battery to No restrictions**
  button visible until YTRear is exempt. It opens
  `ACTION_REQUEST_IGNORE_BATTERY_OPTIMIZATIONS`, falling back to the optimization list and the app
  info page, and the diagnostics panel now reports `Battery optimization: IGNORED|OPTIMIZED`.
- Added a **Quick Settings tile** that turns the rear-screen proxy on or off with one tap. A short
  tap stops the foreground service, clears the proxy, and returns the selected player's own media
  notification; tapping again restarts the proxy and re-snoozes that notification. The tile is
  active only when notification access is granted, a player is configured, and the service is
  running; when setup is incomplete a tap opens YTRear. Duplicate taps delivered by HyperOS are
  debounced.
- Gated auto-detection, snoozing, and notification restoration on the foreground service, so
  turning the proxy off leaves every player's native notification and handoff behavior alone.
- Added launcher icons to the player picker with a pinned, tinted auto-detect row, loaded off the
  main thread through a small `LruCache` so scrolling and repeated searches stay responsive.
- Bumped the candidate to version 1.5.0 (`versionCode 18`).

## 1.4.1 - 2026-11-17

- Expanded `PlayerSelection.NATIVE_REAR_PLAYERS` to match HyperOS's full compiled rear-music
  allowlist (`com.xiaomi.music`, `com.miui.player`, `com.tencent.qqmusic`,
  `com.netease.cloudmusic`, `com.kugou.android`, `cn.kuwo.player`, and `com.spotify.music`), so
  apps that the firmware already drives natively on the rear screen are omitted from both manual
  selection and auto-detection.
- Removed the obsolete `android.permission.SYSTEM_ALERT_WINDOW` permission and historical
  overlay/custom-widget probe components (`OverlayService`, `RearWindow`, `RearNotification`, and
  `rear_widget.xml`), keeping the read-only session, display, and log diagnostics under
  **Advanced**.
- Added a GitHub Actions CI workflow (`.github/workflows/ci.yml`) that runs
  `./gradlew :app:assembleDebug :app:lintDebug` and uploads the built debug APK and lint report on
  pushes and pull requests.
- Bumped the candidate to version 1.4.1 (`versionCode 17`).

## 1.4.0 - 2026-11-17

- Added opt-in **Auto-detect active player** mode (`PlayerSelection.Mode.AUTO`) alongside the
  existing manual selection mode (`Mode.MANUAL` remains the default).
- In auto mode, `MediaHub` observes all eligible active `MediaSession`s and automatically switches
  the allowlisted proxy to whichever player most recently transitioned into `STATE_PLAYING`.
  Current playback stays sticky when paused or during transient track-skip buffering, and rapid
  back-and-forth switches between simultaneously playing sessions are rate-limited.
- Primed `SubScreenCenter`'s `< 200 ms` removal-delay window on the leading edge of audio-focus
  and session-order changes and flushed target switches as immediate session-only updates
  (`promote = false`), keeping the rear MAML card stationary across live player handoffs.
- Automatically restores the previous player's snoozed `MediaStyle` notification (250 ms deadline)
  and snoozes the newly active player's notification for 30 days on every auto handoff, while
  defending top-media rank against restored notifications.
- Added a searchable **Excluded apps** dialog (`Excluded from auto-detect`) on the main screen in
  auto mode so specific apps can be ignored and keep their native notifications.
- Persists the last auto-detected target across process restarts and reboots.
- Bumped the candidate to version 1.4.0 (`versionCode 16`).

## 1.3.2 - 2026-09-13

- Restores the previous player's media notification automatically when the user selects a
  different player.
- Android does not expose direct unsnoozing to ordinary notification listeners, so YTRear shortens
  the previous notification's existing snooze to 250 ms. Android then reposts it normally after
  the new target has already been selected.
- Persists pending restorations until the notification listener is connected, so switching still
  cleans up correctly across listener disconnects or process restarts.
- Verified on-device in both directions. Switching away from actively playing YouTube Music
  removed it from both Android snooze lists and immediately restored its native notification;
  switching back snoozed only YouTube Music again. The pending restoration marker cleared after
  each handoff. If the previous player is not running, its notification returns the next time that
  player posts one.
- Bumped the candidate to version 1.3.2 (`versionCode 15`).

## 1.3.1 - 2026-09-13

- Generalized the stable YouTube Music notification-ranking workaround to the player selected in
  the launch picker.
- YTRear now snoozes that player's original MediaStyle notification for 30 days and supplies its
  proxy notification in its place. This prevents the original card from retaking HyperOS's
  top-media position and collapsing the expanded Dynamic Island during Next or Previous.
- Applies the workaround to an already-active notification immediately when the user switches
  players, when the notification listener connects, and whenever the selected player posts a new
  media notification.
- Verified on-device with Poweramp: its MediaSession remains active, controls continue forwarding,
  its original notification is snoozed, and YTRear's proxy remains active. Spotify remains excluded
  because HyperOS supports it natively.
- Bumped the candidate to version 1.3.1 (`versionCode 14`). The tagged 1.2 stable baseline is
  unchanged.

### Uninstall and notification recovery

YTRear never modifies the selected player's application settings or data. Uninstalling YTRear
stops all future proxying and notification snoozing. Android may retain the currently snoozed media
notification after YTRear is removed; if the player's native notification does not return
immediately, force-stop that player, reopen it, and start playback. This clears the old notification
instance and restores its normal notification and Dynamic Island behavior.
