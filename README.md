# Light Keymapper — source prototype

A small, offline Android Java project demonstrating optional Accessibility Service key filtering and single-tap gesture dispatch. It has no internet permission, ads, analytics, or third-party libraries.

## What this build contains

- Space, E and F key-down to one short tap at configurable screen-percentage coordinates.
- An in-app mapping switch that is OFF by default. The Android Accessibility Service must also be enabled separately.
- Input validation for tap coordinates (0–100%).
- No ADB or Developer Options requirement.

## Important limits

- This is source code, **not a compiled or tested APK**. It has not been tested on a TECNO handset.
- Android must deliver hardware key events to the enabled Accessibility Service. Some OEM builds, games, and input devices may not deliver them as expected.
- While the in-app mapping switch is ON, Space, E and F may be captured globally, not just inside a game. Turn it OFF when not playing.
- Space/E/F produce one 55 ms tap; key holds are not translated into continuous movement.
- No WASD hold-to-move, multi-touch, mouse buttons, mouse-look, analog stick emulation, or game-specific profiles.
- Accessibility gesture dispatch is not equivalent to injecting physical touchscreen input. Some games may ignore or block it. Only enable an accessibility service you understand and trust.
- Screen coordinates are approximate percentages of the real display. System bars, rotation, cutouts, and game scaling can shift targets.

## Build on an Android phone

1. Install a reputable Android IDE/build environment that supports Gradle Android projects. AndroidIDE availability and compatibility can change; use its official project source if available for your device.
2. Extract this ZIP into a folder on your phone.
3. Open/import the folder containing `settings.gradle`.
4. Allow the IDE to download Android Gradle Plugin and SDK components if prompted. Initial setup needs internet; cached dependencies may allow later offline builds.
5. Build the `app` debug variant. The expected output is `app/build/outputs/apk/debug/app-debug.apk`.
6. Install the generated APK. If Android blocks installation, use the system prompt to allow installs from that specific IDE/file manager. Do not disable Play Protect globally.
7. Open Light Keymapper → Open Accessibility Settings → enable the service only if you understand the permission.
8. Return to the app, configure coordinates, save, then enable the in-app mapping switch only while testing.

## Build configuration

- Java; Android Gradle Plugin 8.6.1
- compileSdk 35, targetSdk 32, minSdk 26
- Java 17 is recommended for the Android Gradle Plugin.
- No `INTERNET` permission and no external libraries.

If the build fails due to missing SDK/platform packages or incompatible JDK, follow the IDE's error message and install/select the requested components. This project has not been compiled in the current environment, so a successful build is not guaranteed until built on-device.

## Optional: build the APK in GitHub Actions (no PC needed)

This project includes `.github/workflows/android-build.yml`. After the project is uploaded to a GitHub repository on your account:

1. Open the repository on GitHub and upload the **contents** of the `LightKeyMapper` folder (including the hidden `.github` folder). Keep the `app`, `build.gradle`, and `settings.gradle` files at the repository root inside `LightKeyMapper`'s contents; do not add an extra nested `LightKeyMapper/LightKeyMapper` folder.
2. Open the repository's **Actions** tab and select **Build Android APK**.
3. Tap **Run workflow** if it is available, then wait for the workflow to finish. A green check means the build job completed; a red X means it failed and the logs should be checked.
4. Open the completed run, scroll to **Artifacts**, and download `LightKeyMapper-debug-apk`. Extract the ZIP and install `app-debug.apk` on your phone.

The workflow builds a **debug APK** for testing. It is not a Play Store release and has not been tested on every phone/game. GitHub's connector can work with repositories already accessible to the account, but creating a new repository may need to be done directly on GitHub first.

## Current prototype limitations

This is a minimal proof of concept, not a complete keymapper. It maps selected keyboard key-down events to single screen taps. It does not yet implement continuous WASD movement, multi-touch control, robust mouse-look, or per-game profiles. Accessibility gestures are subject to Android/game restrictions and may not work in every game. Test with mapping disabled first, and enable the service only when you intend to use it.
