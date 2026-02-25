# Installation Guide

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## macOS Installation

## Installation via Homebrew (Recommended)

The easiest installation method.

```bash
# Add Homebrew Tap
brew tap heesubsong/vibesmith

# Install VibeSmith
brew install --cask vibesmith
```

After installation, launch VibeSmith from the Applications folder.

## Installation with DMG File

1. Download the latest `.dmg` file from [GitHub Releases](https://github.com/heesubsong/vibesmith/releases)
2. Open the DMG file
3. Drag the VibeSmith icon to the Applications folder
4. Launch VibeSmith from the Applications folder

## Security Settings

If macOS Gatekeeper warning appears:

1. Open **System Preferences** > **Security & Privacy**
2. Click **Open Anyway** in the **General** tab
3. Or Control + click the app icon > Select **Open**

### ⚠️ Warnings

⚠️ macOS may show a security warning on first launch.
⚠️ Runs natively on Apple Silicon (M1/M2/M3) Macs.

## Windows Installation

## Installation with Installer

1. Download the latest `.exe` file from [GitHub Releases](https://github.com/heesubsong/vibesmith/releases)
2. Run the downloaded installer
3. Follow the installation wizard instructions
4. Launch VibeSmith from the Start menu after installation

## Portable Version

If you want to use without installation:

1. Download the Portable version (`.zip`)
2. Extract to desired folder
3. Run `VibeSmith.exe`

## Permission Settings

If Windows Defender SmartScreen warning appears:

1. Click **More info**
2. Click **Run anyway** button

## Linux Installation

## Installation with AppImage

1. Download the latest `.AppImage` file from [GitHub Releases](https://github.com/heesubsong/vibesmith/releases)
2. Grant execution permission:
   ```bash
   chmod +x VibeSmith-*.AppImage
   ```
3. Run AppImage:
   ```bash
   ./VibeSmith-*.AppImage
   ```

## .deb Package (Ubuntu/Debian)

```bash
# Install downloaded .deb file
sudo dpkg -i vibesmith_*.deb

# Resolve dependencies
sudo apt-get install -f
```

## .rpm Package (Fedora/RHEL)

```bash
# Install downloaded .rpm file
sudo rpm -i vibesmith-*.rpm
```

## Build from Source

For developers who want to build from source.

## Prerequisites

- **Node.js**: 18+
- **npm**: 8+
- **Python**: 3.11+

## Build Steps

```bash
# Clone repository
git clone https://github.com/heesubsong/vibesmith.git
cd vibesmith

# Install dependencies
make setup

# Build desktop app
make dist-desktop

# Built app location:
# - macOS: packages/desktop/dist/VibeSmith.dmg
# - Windows: packages/desktop/dist/VibeSmith.exe
# - Linux: packages/desktop/dist/VibeSmith.AppImage
```

For detailed build guide, see [Developer Documentation](../developer-guide/).

## Verify Installation

After installation is complete, check the following:

## 1. Launch App

When you launch VibeSmith, you should see:
- Dashboard main screen
- Left sidebar (Navigation)
- Top header

## 2. Check Version

You can check the version at **Help** > **About VibeSmith**.

Current latest version: **0.1.0**

## 3. If Problems Occur

If you encounter installation issues:
- [Troubleshooting Guide](98-troubleshooting.md)
- [GitHub Issues](https://github.com/heesubsong/vibesmith-community/issues)
- Check logs: **Help** > **View Logs**

### 💡 Useful Tips

💡 Auto-update will download new versions automatically when enabled.
💡 Use the Portable version to customize the installation location.
💡 Multiple versions can be installed simultaneously for testing.

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0