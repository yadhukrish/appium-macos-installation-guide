# Prerequisites

This document describes all tools required before installing Appium on macOS (Apple Silicon).
Complete every prerequisite in this guide before proceeding to any installation step.

---

## Overview

| Tool | Version | Purpose |
|---|---|---|
| macOS | 13 Ventura+ | Host operating system |
| Xcode | Latest stable | iOS simulator and build tools |
| Android Studio | Latest stable | Android SDK and emulator |
| Homebrew | Latest stable | macOS package manager |
| NVM | Latest stable | Node.js version manager |
| Node.js | 20.19+ | Appium runtime |
| npm | 10+ | Appium package installer |
| Python | 3.8+ | Validation script runtime |

---

## macOS Version

Appium 3.x on Apple Silicon requires macOS 13 Ventura or later.

Check your macOS version:

```bash
sw_vers
```

Expected output:

```
ProductName:    macOS
ProductVersion: 14.x.x
BuildVersion:   23xxxxx
```

If your version is below 13, update via:

```
System Settings → General → Software Update
```

---

## Xcode

Xcode provides the iOS Simulator, build tools, and the XCUITest automation framework
that Appium's iOS driver depends on.

Install Xcode from the Mac App Store:

```
https://apps.apple.com/app/xcode/id497799835
```

> **Note:** Xcode is a large download (~10 GB). Install this first while setting up
> other prerequisites.

Verify installation:

```bash
xcode-select -p
```

Expected output:

```
/Applications/Xcode.app/Contents/Developer
```

Accept the Xcode license agreement — skipping this causes a cryptic error the first
time any Xcode tool runs:

```bash
sudo xcodebuild -license accept
```

Install Xcode Command Line Tools — these provide compilers and build utilities
that Appium's iOS driver depends on:

```bash
xcode-select --install
```

---

## Android Studio

Android Studio provides the Android SDK, ADB (Android Debug Bridge), and the
emulator that Appium's Android driver depends on.

Download Android Studio:

```
https://developer.android.com/studio
```

During setup, ensure the following components are selected in the SDK Manager:

| Component | Purpose |
|---|---|
| Android SDK | Core Android platform tools |
| Android SDK Platform Tools | Provides `adb` command |
| Android Emulator | Virtual Android device |
| Android SDK Build Tools | Required for app compilation |

Verify ADB is accessible after installation:

```bash
adb version
```

Expected output:

```
Android Debug Bridge version 1.0.41
Version 35.x.x
```

---

## Disk Space and RAM

Appium with both iOS and Android environments requires significant disk space.

| Requirement | Minimum |
|---|---|
| RAM | 8 GB |
| Free Disk Space | 20 GB |

Check available disk space:

```bash
df -h /
```

---

## Internet Connection

An active internet connection is required throughout the installation process for:

- Downloading Homebrew, NVM, Node.js
- Installing Appium and its drivers via npm
- Downloading Android SDK components via Android Studio
- Downloading iOS Simulator runtimes via Xcode

---

## Next Step

Once all prerequisites are in place, proceed to [Install Node.js](install-node.md).
