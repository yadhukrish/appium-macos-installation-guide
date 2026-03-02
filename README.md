# Appium Setup on macOS (Apple Silicon)

![macOS](https://img.shields.io/badge/macOS-Apple%20Silicon-black?logo=apple)
![Node.js](https://img.shields.io/badge/Node.js-LTS-green?logo=node.js)
![Appium](https://img.shields.io/badge/Appium-Latest-blue)
![Platforms](https://img.shields.io/badge/Platforms-iOS%20%7C%20Android-purple)
![License](https://img.shields.io/badge/License-Educational-lightgrey)


---
## Quick Navigation

| Section | Link |
|-------|------|
| Supported Environment | [Go](#supported-environment) |
| System Requirements | [Go](#system-requirements) |
| Install Node.js | [Go](#install-nodejs-using-nvm) |
| Install Appium | [Go](#install-appium) |
| iOS Setup | [Go](#ios-environment-setup) |
| Android Setup | [Go](#android-environment-setup) |
| Validation Script | [Go](#python-validation-script) |
| Troubleshooting | [Go](#troubleshooting) |

---


A **step-by-step guide for installing and configuring Appium on macOS** for **iOS and Android mobile automation testing**.

This repository is designed as part of a **QA / Mobile Automation Engineering portfolio** and follows **industry-standard technical writing practices**.

The goal is to provide a **clean, reproducible Appium setup for Apple Silicon Macs (M1 / M2 / M3 / newer)**.

---

## Target Audience

- Beginners learning mobile automation
- QA Engineers transitioning to automation
- Mobile Automation Engineers setting up a local environment

---
## Table of Contents

- [Supported Environment](#supported-environment)
- [System Requirements](#system-requirements)
- [Prerequisites](#prerequisites)
- [Install Homebrew](#install-homebrew)
- [Install Node.js Using NVM](#install-nodejs-using-nvm)
- [Install Appium](#install-appium)
- [Install Appium Drivers](#install-appium-drivers)
- [iOS Environment Setup](#ios-environment-setup)
- [Android Environment Setup](#android-environment-setup)
- [Configure Environment Variables](#configure-environment-variables)
- [Verify Installation](#verify-installation)
- [Python Validation Script](#python-validation-script)
- [Troubleshooting](#troubleshooting)
- [Useful Resources](#useful-resources)


---
## Quick Start

If you want to get Appium running quickly, follow these minimal steps.

### 1. Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Install NVM and Node.js

```bash
brew install nvm
mkdir ~/.nvm
```

Add NVM to your shell:

```bash
export NVM_DIR="$HOME/.nvm"
source $(brew --prefix nvm)/nvm.sh
```

Reload the shell:

```bash
source ~/.zshrc
```

Install Node.js:

```bash
nvm install --lts
```

### 3. Install Appium

```bash
npm install -g appium
```

### 4. Install Drivers

```bash
appium driver install xcuitest
appium driver install uiautomator2
```

### 5. Start Appium

```bash
appium
```

If the server starts successfully, your environment is ready.


---
## Appium Architecture Overview

The following diagram shows how Appium interacts with mobile platforms.
flowchart TD

TestScript["Test Script (Python / Java / JS)"]
Client["Appium Client Library"]
Server["Appium Server"]
Driver["Appium Driver (XCUITest / UIAutomator2)"]
Platform["Mobile Platform APIs"]
Device["Device / Emulator / Simulator"]
App["Mobile Application"]

TestScript --> Client
Client --> Server
Server --> Driver
Driver --> Platform
Platform --> Device
Device --> App


### Architecture Explanation

| Component | Description |
|----------|-------------|
| Test Script | Automation test written in Python, Java, or JavaScript |
| Client Library | Sends automation commands to Appium |
| Appium Server | Receives and routes automation commands |
| Appium Driver | Platform-specific driver (XCUITest or UIAutomator2) |
| Platform APIs | iOS or Android automation frameworks |
| Device | Physical device, emulator, or simulator |
| App | Application under test |


## Automation Test Execution Flow

The following diagram illustrates how a test travels through the automation stack.
sequenceDiagram

participant TestScript
participant AppiumClient
participant AppiumServer
participant Driver
participant Device

TestScript->>AppiumClient: Send automation command
AppiumClient->>AppiumServer: HTTP request
AppiumServer->>Driver: Forward command
Driver->>Device: Execute platform automation
Device-->>Driver: Response
Driver-->>AppiumServer: Result
AppiumServer-->>AppiumClient: Response
AppiumClient-->>TestScript: Test result

---

## What This Guide Covers

- Installing **Node.js using NVM**
- Installing **Appium (latest stable version)**
- Installing **Appium drivers**
- Configuring **iOS automation**
- Configuring **Android automation**
- Running a **Python validation test**

---

## Supported Environment

| Component | Requirement |
|-----------|-------------|
| macOS | Any recent version |
| Architecture | Apple Silicon (M1 / M2 / M3 / newer) |
| Appium | Latest stable version |
| Node.js | Managed via NVM |
| Platforms | iOS and Android |

---

### Check macOS Version

```bash
sw_vers
```

If your system is outdated, update macOS from:

System Settings → General → Software Update

---

## System Requirements

Ensure your system meets the following requirements.

| Requirement | Details |
|-------------|--------|
| RAM | Minimum 8 GB |
| Disk Space | Minimum 20 GB |
| Internet | Required for dependency downloads |

These requirements ensure **stable Android emulators and iOS simulators**.

---

## Prerequisites

The following tools must be installed before setting up Appium.

| Tool | Purpose |
|-----|--------|
| Homebrew | macOS package manager |
| NVM | Node version manager |
| Node.js | Runtime environment for Appium |
| Xcode | Required for iOS automation |
| Android Studio | Required for Android automation |

---

## Install Homebrew

Homebrew simplifies installation of developer tools.

Install Homebrew:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify installation:

```bash
brew --version
```

---

## Install Node.js Using NVM

Using **NVM (Node Version Manager)** avoids dependency conflicts.

### Install NVM

```bash
brew install nvm
```

Create the NVM directory:

```bash
mkdir ~/.nvm
```

Open your shell configuration file:

```bash
nano ~/.zshrc
```

Add the following lines:

```bash
export NVM_DIR="$HOME/.nvm"
source $(brew --prefix nvm)/nvm.sh
```

Reload the shell:

```bash
source ~/.zshrc
```

### Install Node.js (LTS)

```bash
nvm install --lts
```

Verify installation:

```bash
node -v
npm -v
```

---

## Install Appium

Install the latest stable version of Appium globally.

```bash
npm install -g appium
```

Verify installation:

```bash
appium -v
```

Run Appium Doctor:

```bash
npx appium-doctor
```

---

## Install Appium Drivers

Appium uses a **driver-based architecture**.

### List available drivers

```bash
appium driver list --updates
```

### Install iOS Driver

```bash
appium driver install xcuitest
```

### Install Android Driver

```bash
appium driver install uiautomator2
```

Verify installed drivers:

```bash
appium driver list --installed
```

---

## iOS Environment Setup

iOS automation requires **Xcode** and **iOS simulators**.

### Install Xcode

Download Xcode from the **Mac App Store**.

Verify installation:

```bash
xcode-select -p
```

Accept the license agreement:

```bash
sudo xcodebuild -license accept
```

Install command line tools:

```bash
xcode-select --install
```

### Verify iOS Simulators

```bash
xcrun simctl list devices
```

### Screenshot

![Xcode Simulators](docs/images/xcode-simulators.png)

---

## Android Environment Setup

Android automation requires **Android Studio** and the **Android SDK**.

### Install Android Studio

Download Android Studio:

https://developer.android.com/studio

Install the following components:

- Android SDK
- Android SDK Platform Tools
- Android Emulator
- Android SDK Build Tools

### Verify ADB Installation

```bash
adb version
```

Check connected devices:

```bash
adb devices
```

### Screenshot

![Android Emulator](docs/images/android-emulator.png)

---

## Configure Environment Variables

Add Android SDK paths to your shell configuration.

Open your shell profile:

```bash
nano ~/.zshrc
```

Add the following lines:

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$ANDROID_HOME/emulator:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/tools:$PATH
```

Reload the shell:

```bash
source ~/.zshrc
```

---

## Verify Installation

Start the Appium server:

```bash
appium
```

Expected output:

```
Appium REST http interface listener started
```

Verify installed drivers:

```bash
appium driver list --installed
```

Run Appium doctor:

```bash
npx appium-doctor
```

---

## Python Validation Script

Install the Appium Python client:

```bash
pip install Appium-Python-Client
```

Example validation script:

```python
from appium import webdriver

caps = {
    "platformName": "Android",
    "deviceName": "Android Emulator",
    "automationName": "UiAutomator2",
    "appPackage": "com.android.settings",
    "appActivity": ".Settings"
}

driver = webdriver.Remote("http://127.0.0.1:4723", caps)

print("App launched successfully!")

driver.quit()
```

Run the script:

```bash
python scripts/python/test_appium.py
```

---

## Troubleshooting

## Troubleshooting

<details>
<summary>Node Version Issues</summary>

Check Node version:

```bash
node -v
```

Switch Node version:

```bash
nvm use --lts
```

</details>

---

<details>
<summary>Android Device Not Detected</summary>

Restart ADB:

```bash
adb kill-server
adb start-server
```

Verify devices:

```bash
adb devices
```

</details>

---

<details>
<summary>Appium Doctor Errors</summary>

Run Appium Doctor:

```bash
npx appium-doctor
```

Follow the recommended fixes.

</details>
---

## Useful Resources

Appium Documentation  
https://appium.io/docs/en/latest/

Appium GitHub  
https://github.com/appium/appium

Android Developer Documentation  
https://developer.android.com

Apple Developer Documentation  
https://developer.apple.com

---

## License

This project is provided for **educational and portfolio purposes**.
