# Implementation Plan - Fix API 37 Build Error

The error `Failed to find Platform SDK with path: platforms;android-37` occurs because the installed SDK for API 37 is specifically version `37.0` (as seen in `platforms;android-37.0`), while standard Gradle configurations look for a package named exactly `android-37`. This is due to Android's new "Minor SDK" release model.

## User Review Required

> [!IMPORTANT]
> To support API 37 (Android 17) correctly, the official recommendation is to upgrade **Android Gradle Plugin (AGP)** to **8.9.0-rc01** or higher. However, I will first try a less invasive fix by targeting the specific minor SDK version or using the preview codename.

## Proposed Changes

### [Component Name] :app Build Configuration

#### [MODIFY] [build.gradle](file:///C:/Users/jithi/OneDrive/Desktop/mountzoft/GenderClassifierWithTensorFlow/app/build.gradle)
- Try targeting API 37 using the specific minor version syntax if supported by AGP 8.5.2, or use the "CinnamonBun" codename.
- If that fails, I will attempt to "patch" the SDK directory to make it recognizable by renaming the folder and updating `source.properties`.

## Verification Plan

### Automated Tests
- Run `./gradlew :app:assembleDebug` after each configuration attempt.

### Manual Verification
- Verify that the "Platform SDK not found" error disappears in the IDE.
