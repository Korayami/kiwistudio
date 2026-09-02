# Building KiwiStudio

This document provides complete, step-by-step instructions for building **KiwiStudio** into runnable executables, installers, and distribution packages across Windows, macOS, and Linux platforms.

---

## 1. Prerequisites

Before building KiwiStudio, ensure your environment meets the prerequisites for your host platform.

### Common Requirements (All Platforms)
- **Node.js**: Version 20.x or 22.x (LTS recommended)
- **npm**: Installed with Node.js
- **Python**: Python 3.x (required for compiling native Node modules)
- **Git**: Latest version

### Platform-Specific Tooling

#### Windows:
- **Visual Studio Build Tools** (2022 or 2019):
  - Workload: *Desktop development with C++*
  - Windows 10/11 SDK
- **Inno Setup 6** (optional, required if generating `.exe` setup installers):
  - Download and install [Inno Setup 6](https://jrsoftware.org/isdl.php). Ensure `ISCC.exe` is added to your PATH or installed in default locations.

#### macOS:
- **Xcode Command Line Tools**:
  - Install via terminal: `xcode-select --install`

#### Linux (Debian / Ubuntu / Fedora / Arch):
- Build tools and development libraries:
  ```bash
  # Debian / Ubuntu / Linux Mint:
  sudo apt-get update
  sudo apt-get install -y build-essential g++ pkg-config libsecret-1-dev libx11-dev libxkbfile-dev fakeroot rpm snapcraft

  # Fedora / RHEL / CentOS:
  sudo dnf groupinstall "Development Tools"
  sudo dnf install libsecret-devel libX11-devel libxkbfile-devel rpm-build
  ```

---

## 2. Initial Setup

1. **Clone the repository** (if not already done):
   ```bash
   git clone <repository-url>
   cd KiwiStudio
   ```

2. **Install project dependencies**:
   ```bash
   npm install
   ```

3. **Compile client source code**:
   ```bash
   npm run compile
   ```

---

## 3. Building Runnable Executables & Packages

KiwiStudio uses Gulp tasks to package Electron binaries and produce standalone executables and distribution packages.

---

### A. Windows Build Instructions

#### 1. Runnable Executable Folder (Standalone `.exe`)
To package KiwiStudio into a portable directory containing `KiwiStudio.exe`:

- **Windows x64 (64-bit)**:
  ```bash
  npm run gulp -- vscode-win32-x64
  ```
  *Output location:* `../VSCode-win32-x64` (relative to repo root), containing `KiwiStudio.exe` and associated runtime files.

- **Windows ARM64**:
  ```bash
  npm run gulp -- vscode-win32-arm64
  ```
  *Output location:* `../VSCode-win32-arm64`

#### 2. Windows Installer (`.exe` Setup File via Inno Setup)
After generating the executable folder above:

- **System-wide Installer (x64)**:
  ```bash
  npm run gulp -- vscode-win32-x64-system-setup
  ```
- **User-level Installer (x64)**:
  ```bash
  npm run gulp -- vscode-win32-x64-user-setup
  ```
*Output location:* `.build/win32-x64/system-setup/` or `.build/win32-x64/user-setup/`

---

### B. macOS Build Instructions (MacBook Air / Pro / Mac mini / Studio)

#### 1. Runnable `.app` Bundle
Build standalone macOS application bundles for Apple Silicon (M1/M2/M3/M4) or Intel Macs:

- **Apple Silicon (ARM64)**:
  ```bash
  npm run gulp -- vscode-darwin-arm64
  ```
  *Output location:* `../VSCode-darwin-arm64/KiwiStudio.app`

- **Intel Macs (x64)**:
  ```bash
  npm run gulp -- vscode-darwin-x64
  ```
  *Output location:* `../VSCode-darwin-x64/KiwiStudio.app`

#### 2. Distributable `.dmg` or `.zip` Archive

- **Zip Package**:
  ```bash
  cd ../VSCode-darwin-arm64
  zip -r KiwiStudio-macOS-arm64.zip KiwiStudio.app
  ```

- **DMG Installer Image**:
  Create a DMG file using macOS native `hdiutil`:
  ```bash
  hdiutil create -volname "KiwiStudio" \
    -srcfolder "../VSCode-darwin-arm64/KiwiStudio.app" \
    -ov -format UDZO KiwiStudio-macOS-arm64.dmg
  ```

---

### C. Linux Build Instructions

#### 1. Portable Standalone Folder / `.tar.gz`
- **Linux x64**:
  ```bash
  npm run gulp -- vscode-linux-x64
  ```
  *Output location:* `../VSCode-linux-x64` containing the executable binary `kiwistudio`.

  To create a tarball archive:
  ```bash
  tar -czvf KiwiStudio-linux-x64.tar.gz -C ../ VSCode-linux-x64
  ```

- **Linux ARM64 / ARMhf**:
  ```bash
  npm run gulp -- vscode-linux-arm64
  # or for ARMhf:
  npm run gulp -- vscode-linux-armhf
  ```

#### 2. Debian / Ubuntu Package (`.deb`)
```bash
# Prepare deb package structure
npm run gulp -- vscode-linux-x64-prepare-deb

# Build .deb installer file
npm run gulp -- vscode-linux-x64-build-deb
```
*Output location:* `.build/linux/deb/amd64/deb/kiwistudio-amd64.deb`

#### 3. RedHat / Fedora / RHEL Package (`.rpm`)
```bash
# Prepare rpm package structure
npm run gulp -- vscode-linux-x64-prepare-rpm

# Build .rpm installer file
npm run gulp -- vscode-linux-x64-build-rpm
```
*Output location:* `.build/linux/rpm/x86_64/`

#### 4. Snap Package (`.snap`)
```bash
# Build Snap package using snapcraft
npm run gulp -- vscode-linux-x64-build-snap
```
*Output location:* `.build/linux/snap/x64/`

#### 5. AppImage
To bundle the portable Linux output into an AppImage:
1. Download `appimagetool` from [AppImage GitHub Releases](https://github.com/AppImage/AppImageKit/releases).
2. Package `../VSCode-linux-x64` using `appimagetool`:
   ```bash
   ./appimagetool-x86_64.AppImage ../VSCode-linux-x64 KiwiStudio-x86_64.AppImage
   ```

---

## 4. Development & Live Execution

To run KiwiStudio directly in development mode without building full production packages:

```bash
# Watch and compile changes
npm run watch

# In a separate terminal, launch Electron app
npm run electron
```

Or for web server version:
```bash
./scripts/code-server.sh
```
