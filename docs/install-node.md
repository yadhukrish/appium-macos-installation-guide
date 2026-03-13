# Install Node.js Using NVM

This guide installs Node.js via NVM (Node Version Manager). Using NVM rather than
installing Node.js directly lets you switch between Node.js versions without
reinstalling — useful when working across multiple projects with different requirements.

**Prerequisite:** Homebrew must be installed. See [Prerequisites](prerequisites.md).

---

## Install Homebrew

If Homebrew is not already installed:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify installation:

```bash
brew --version
```

Expected output:

```
Homebrew 4.x.x
```

---

## Install NVM

NVM is distributed via Homebrew on macOS:

```bash
brew install nvm
```

Create the NVM working directory — NVM stores all Node.js versions here:

```bash
mkdir ~/.nvm
```

---

## Configure Your Shell Profile

Add NVM to your shell profile so it loads automatically in every new terminal session.
Open your shell configuration file:

```bash
nano ~/.zshrc
```

Add the following lines at the end of the file — the first tells your shell where NVM
lives, the second activates it:

```bash
export NVM_DIR="$HOME/.nvm"
source $(brew --prefix nvm)/nvm.sh
```

Save and close the file (`Ctrl+O`, `Enter`, `Ctrl+X`).

Reload your shell to apply the changes:

```bash
source ~/.zshrc
```

Verify NVM is active:

```bash
nvm --version
```

Expected output:

```
0.39.x
```

---

## Install Node.js

Install the latest LTS (Long Term Support) version of Node.js — Appium 3.x requires
Node.js 20.19 or later. LTS versions are recommended for stability:

```bash
nvm install --lts
```

Set it as the default version for all terminal sessions:

```bash
nvm alias default --lts
```

Verify both Node.js and npm are installed correctly:

```bash
node -v
npm -v
```

Expected output:

```
v20.x.x
10.x.x
```

> **Note:** If `node -v` returns `command not found` after running the above steps,
> close your terminal completely, reopen it, and run `source ~/.zshrc` again.

---

## Why NVM Instead of Direct Installation?

Installing Node.js directly via Homebrew (`brew install node`) ties you to a single
version managed by Homebrew's update cycle. NVM gives you explicit control — you can
install, switch, and pin Node.js versions per project using a `.nvmrc` file.

For Appium specifically, version requirements change between major releases. NVM makes
upgrading or downgrading Node.js a single command rather than a full reinstall.

---

## Next Step

Proceed to [Install Appium](install-appium.md).
