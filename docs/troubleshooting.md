# Troubleshooting

This guide covers the most common errors encountered when setting up Appium 3.x
on macOS (Apple Silicon) and their exact fixes.

---

## Error Index

- [NVM command not found after installation](#1-nvm-command-not-found-after-installation)
- [Android device not detected by ADB](#2-android-device-not-detected-by-adb)
- [Appium Doctor reports ANDROID_HOME not set](#3-appium-doctor-reports-android_home-not-set)
- [XCUITest driver fails — Xcode license not accepted](#4-xcuitest-driver-fails--xcode-license-not-accepted)
- [Port 4723 already in use](#5-port-4723-already-in-use)

---

## 1. NVM command not found after installation

**Symptom:**

```
zsh: command not found: nvm
```

**Cause:** The NVM shell configuration was not added to `~/.zshrc`, or the shell
was not reloaded after editing the file.

**Fix:**

Verify the NVM lines exist in your shell profile:

```bash
cat ~/.zshrc | grep NVM
```

If nothing is returned, add them manually:

```bash
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo 'source $(brew --prefix nvm)/nvm.sh' >> ~/.zshrc
```

Reload the shell:

```bash
source ~/.zshrc
```

Verify NVM is now available:

```bash
nvm --version
```

---

## 2. Android device not detected by ADB

**Symptom:**

```bash
adb devices
```

Returns:

```
List of devices attached
emulator-5554   offline
```

or returns an empty list with no devices.

**Cause:** The ADB server is in a stale state, or the emulator has not fully booted.

**Fix:**

Reset the ADB server:

```bash
adb kill-server
adb start-server
```

Wait for the emulator to reach the home screen, then recheck:

```bash
adb devices
```

Expected output after fix:

```
List of devices attached
emulator-5554   device
```

> **Note:** `offline` means ADB can see the device but cannot communicate with it.
> `device` means the connection is active and ready.

---

## 3. Appium Doctor reports ANDROID_HOME not set

**Symptom:**

```
✖ ANDROID_HOME is NOT set!
```

**Cause:** The Android SDK environment variable was not added to `~/.zshrc`, or
the shell was not reloaded after editing.

**Fix:**

Open your shell profile:

```bash
nano ~/.zshrc
```

Verify or add the following lines:

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$ANDROID_HOME/emulator:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/tools:$PATH
```

Save and reload:

```bash
source ~/.zshrc
```

Verify the variable is now set:

```bash
echo $ANDROID_HOME
```

Expected output:

```
/Users/your-username/Library/Android/sdk
```

Re-run Appium Doctor to confirm the fix:

```bash
npx appium-doctor
```

---

## 4. XCUITest driver fails — Xcode license not accepted

**Symptom:**

```
You have not agreed to the Xcode license agreements.
You must agree to both license agreements below in order to use Xcode.
```

or a test session fails immediately with no clear error.

**Cause:** The Xcode license was never accepted after installation. This causes
any tool in the Xcode toolchain — including Appium's XCUITest driver — to fail.

**Fix:**

Accept the license from the command line:

```bash
sudo xcodebuild -license accept
```

You will be prompted for your macOS password. After accepting, verify the Xcode
tools are accessible:

```bash
xcode-select -p
```

Expected output:

```
/Applications/Xcode.app/Contents/Developer
```

---

## 5. Port 4723 already in use

**Symptom:**

```
Error: listen EADDRINUSE: address already in use 127.0.0.1:4723
```

**Cause:** A previous Appium server session did not shut down cleanly and is still
holding port 4723.

**Fix:**

Find the process occupying the port:

```bash
lsof -i :4723
```

Expected output:

```
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
node     1234 user   xx   IPv4 xxxxx      0t0  TCP *:4723 (LISTEN)
```

Kill the process using its PID:

```bash
kill -9 1234
```

Restart Appium:

```bash
appium
```

Alternatively, start Appium on a different port to avoid the conflict:

```bash
appium --port 4800
```

> **Note:** If you use a custom port, update your test script's Remote URL to match:
> `http://127.0.0.1:4800`

---

## Still Stuck?

Run Appium Doctor for a full environment diagnostic:

```bash
npx appium-doctor
```

Check the official Appium discussion forum:

```
https://discuss.appium.io
```

File an issue on the Appium GitHub repository:

```
https://github.com/appium/appium/issues
```
