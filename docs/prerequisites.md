# Prerequisites

Before installing Appium on macOS, ensure that the required dependencies are installed and properly configured.

This section describes the tools required to run Appium successfully.

---

## System Requirements

| Component | Requirement |
|-----------|-------------|
| Operating System | macOS 11 or later |
| Package Manager | Homebrew |
| Runtime Environment | Node.js (v16 or later) |
| Package Manager | npm |

---

## Install Homebrew

Homebrew is a package manager for macOS that simplifies the installation of development tools.

### Install Homebrew

Run the following command in Terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Verify Installation

```bash
brew --version
```

Example output:

```
Homebrew 4.x.x
```

---

## Install Node.js

Appium runs on Node.js, so it must be installed before installing Appium.

### Install Node.js

```bash
brew install node
```

### Verify Installation

Check the Node.js version:

```bash
node -v
```

Check the npm version:

```bash
npm -v
```

Example output:

```
v20.x.x
10.x.x
```

---

## Install Appium Doctor

Appium Doctor verifies whether your environment is properly configured.

### Install Appium Doctor

```bash
npm install -g appium-doctor
```

### Run Appium Doctor

```bash
appium-doctor
```

The tool checks for required dependencies and reports any missing components.

---

## Optional Dependencies

Depending on the platform you want to test, additional tools may be required.

### Android Testing

For Android automation:

- Install Android Studio
- Install Android SDK
- Configure environment variables

### iOS Testing

For iOS automation:

- Install Xcode
- Install Xcode Command Line Tools
- Configure developer certificates

---

## Next Step

After completing the prerequisites, proceed to the next section:

➡ **[Install Node.js](install-node.md)**
