# WIFI SENTINEL

A defensive Wi-Fi visibility and diagnostics app for Android, written in Kotlin + Jetpack Compose.

## Target device
- Samsung Galaxy S10+ (SM-G975 family)
- Android 15 custom ROM (including EternityROM v5.5, subject to ROM permission/API behavior)
- `compileSdk = 35`, `targetSdk = 35`, `minSdk = 26`

This app uses public Android Wi-Fi APIs. It does **not** crack passwords, bypass network security, deauthenticate devices, capture traffic, or access networks without permission.

## Features
- Scan nearby Wi-Fi access points using Android's Wi-Fi scan API
- Show SSID, BSSID, frequency, channel, signal level, and advertised security type
- Refresh scan results and indicate Android throttling/stale results
- Local connection diagnostics (connected SSID when Android permits)
- Generate random strong passphrases locally
- No account, analytics, cloud service, or backend

## Requirements
- Android Studio Ladybug or newer
- JDK 17
- Android SDK Platform 35
- Gradle 8.11.1 (Android Gradle Plugin 8.9.2 compatible)
- Device/emulator running Android 8.0+; Wi-Fi scan behavior varies by vendor/ROM

## Open and run
1. Extract the ZIP.
2. Open the `WIFI_SENTINEL` folder in Android Studio.
3. Allow Gradle sync to finish and install Android SDK 35 if prompted.
4. Connect the S10+ with USB debugging enabled, or use an Android 15 emulator.
5. Press **Run**.

If you prefer the command line:
```bash
gradle assembleDebug
gradle testDebugUnitTest
```
Install the APK:
```bash
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

## Permissions and Android 15 notes
- `ACCESS_FINE_LOCATION` is required to retrieve nearby scan results on Android versions where the platform gates scan data behind location.
- `NEARBY_WIFI_DEVICES` is declared for Android 13+ Wi-Fi-related access. The app still requests fine location because scan results require it on supported Android releases.
- Android location services may need to be enabled for scan results.
- Android restricts how frequently apps can initiate scans. A refresh can return cached results or be throttled; this is an OS policy, not an app failure.
- On custom ROMs, permission behavior, location toggles, and Wi-Fi HAL support can differ. If the scan list is empty, verify permissions and location services, then test on another Android 15 build.
- SSIDs can be hidden or redacted by Android. BSSID display may be unavailable.
- Android does not expose every router setting or a definitive vulnerability verdict. Security labels are based only on the advertised capabilities returned by the OS.

## Project structure
```text
app/src/main/
  AndroidManifest.xml
  java/com/carter/wifisentinel/
    MainActivity.kt
    data/WifiScanner.kt
    data/WifiModels.kt
    security/PassphraseGenerator.kt
    ui/SentinelViewModel.kt
    ui/SentinelScreen.kt
    ui/theme/Theme.kt
app/src/test/
  java/com/carter/wifisentinel/
    PassphraseGeneratorTest.kt
    WifiFormattingTest.kt
```

## Tests
Run:
```bash
gradle testDebugUnitTest
```
Tests cover channel mapping, security label mapping, and passphrase generation properties. Device Wi-Fi scanning requires a physical device or emulator and is not fully covered by JVM unit tests.

## Privacy
All scan results remain in app memory. The app does not persist or upload SSIDs/BSSIDs. Treat network identifiers as potentially sensitive and share screenshots/reports carefully.

## Troubleshooting
- **Permission denied:** grant Location and Nearby Wi-Fi Devices permissions in Android Settings.
- **No networks:** enable Location services, turn Wi-Fi on, move to an area with visible access points, and retry after a short wait.
- **Stale scan results:** Android may throttle scans; wait before refreshing.
- **Gradle sync fails:** use JDK 17 and install Android SDK 35; update Android Studio if needed.
