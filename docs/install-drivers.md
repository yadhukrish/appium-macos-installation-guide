# Install Appium Drivers

Appium 3.x uses a driver model — the core server handles communication, but each
platform (iOS, Android) requires its own driver installed separately. This keeps
the core server lightweight and lets drivers version independently.

**Prerequisite:** Appium 3.x must be installed. See [Install Appium](install-appium.md).

---

## Available Drivers

| Driver | Platform | Install Name |
|---|---|---|
| XCUITest | iOS / iPadOS | `xcuitest` |
| UIAutomator2 | Android | `uiautomator2` |

---

## Check Available Drivers

List all available drivers and whether updates are pending:

```bash
appium driver list --updates
```

Expected output:

```
✔ Listing available drivers
- uiautomator2 [not installed] (latest: x.x.x)
- xcuitest [not installed] (latest: x.x.x)
```

---

## Install iOS Driver (XCUITest)

XCUITest is Apple's native UI testing framework. Appium's XCUITest driver wraps it
to enable cross-language test automation against iOS simulators and real devices.

```bash
appium driver install xcuitest
```

Expected output:

```
✔ Installing 'xcuitest' using NPM install spec 'appium-xcuitest-driver'
ℹ Driver xcuitest@x.x.x successfully installed
```

---

## Install Android Driver (UIAutomator2)

UIAutomator2 is Google's Android UI testing framework. Appium's UIAutomator2 driver
wraps it to enable automation against Android emulators and real devices.

```bash
appium driver install uiautomator2
```

Expected output:

```
✔ Installing 'uiautomator2' using NPM install spec 'appium-uiautomator2-driver'
ℹ Driver uiautomator2@x.x.x successfully installed
```

---

## Verify Installed Drivers

Confirm both drivers are installed and show their versions:

```bash
appium driver list --installed
```

Expected output:

```
✔ Listing installed drivers
- xcuitest@x.x.x [installed (npm)]
- uiautomator2@x.x.x [installed (npm)]
```

---

## Update Drivers

Drivers version independently from the Appium server. Check for and apply updates
regularly to stay compatible with new iOS and Android OS releases:

```bash
appium driver update xcuitest
appium driver update uiautomator2
```

---

## Why Are Drivers Separate?

In Appium 1.x, all platform support was bundled into the server — updating Appium
meant updating everything at once. Appium 2.x and 3.x split drivers out so:

- iOS and Android drivers can release fixes independently
- You only install the drivers your project actually needs
- Driver updates don't require a full Appium server update

---

## Next Step

Proceed to [Start Server](start-server.md).
