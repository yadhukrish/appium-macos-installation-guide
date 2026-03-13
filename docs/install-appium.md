# Install Appium

This guide installs the Appium 3.x server globally using npm.

**Prerequisite:** Node.js 20.19+ and npm 10+ must be installed. See [Install Node.js](install-node.md).

---

## Install Appium

Install Appium globally so the `appium` command is available from any directory:

```bash
npm install -g appium
```

> **Note:** The `-g` flag installs Appium as a global npm package. Without it,
> Appium would only be accessible from the directory where you ran the command.

Verify the installation:

```bash
appium -v
```

Expected output:

```
3.2.0
```

---

## Run Appium Doctor

Appium Doctor checks your environment for missing dependencies and misconfigurations
before you attempt any automation. Run it immediately after installation — it saves
significant debugging time later.

```bash
npx appium-doctor
```

Appium Doctor checks for:

| Check | What It Validates |
|---|---|
| Node.js version | Meets Appium 3.x minimum requirement |
| npm version | Meets Appium 3.x minimum requirement |
| Xcode | Installed and licensed (iOS) |
| Android SDK | Installed and accessible (Android) |
| Environment variables | `ANDROID_HOME` and `PATH` entries |

Expected output (all checks passing):

```
info AppiumDoctor Appium Doctor v.x.x.x
info AppiumDoctor ### Diagnostic for necessary dependencies starting ###
info AppiumDoctor  ✔ The Node.js binary was found at: /Users/xxx/.nvm/versions/node/vxx/bin/node
info AppiumDoctor  ✔ Node version is x.x.x
info AppiumDoctor  ✔ Xcode is installed at: /Applications/Xcode.app/Contents/Developer
info AppiumDoctor  ✔ Xcode Command Line Tools are installed.
info AppiumDoctor  ✔ DevToolsSecurity is enabled.
info AppiumDoctor  ✔ The Authorization DB is set up properly.
info AppiumDoctor  ✔ Java Development Kit (JDK) installed at: ...
info AppiumDoctor  ✔ ANDROID_HOME is set to: /Users/xxx/Library/Android/sdk
info AppiumDoctor  ✔ JAVA_HOME is set to: ...
info AppiumDoctor ### Diagnostic for necessary dependencies completed, no fix needed. ###
```

> **Note:** Warnings (⚠) are non-blocking — Appium will still run. Errors (✖) must
> be resolved before the affected platform will work.

---

## Configure Environment Variables

These variables tell your system where the Android SDK is installed so that tools
like `adb` and the emulator can be called from any terminal window.

Open your shell profile:

```bash
nano ~/.zshrc
```

Add the following — each `PATH` line exposes a different set of Android tools
to your terminal:

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$ANDROID_HOME/emulator:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/tools:$PATH
```

Save and reload your shell:

```bash
source ~/.zshrc
```

Verify the variable is set:

```bash
echo $ANDROID_HOME
```

Expected output:

```
/Users/your-username/Library/Android/sdk
```

---

## Appium 2.x vs 3.x — Key Differences

If you have used Appium before, note these breaking changes in Appium 3.x:

| Area | Appium 2.x | Appium 3.x |
|---|---|---|
| Default port | 4723 | 4723 (unchanged) |
| Capabilities format | Plain dict or `Options` | `Options` class required |
| Driver installation | Separate step | Separate step (unchanged) |
| Node.js requirement | 14+ | 20.19+ |
| Plugin system | Available | Available (unchanged) |

---

## Next Step

Proceed to [Install Drivers](install-drivers.md).
