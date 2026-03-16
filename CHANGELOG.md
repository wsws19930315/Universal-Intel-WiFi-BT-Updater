# Changelog

All notable changes to the Universal Intel Wi-Fi and Bluetooth Drivers Updater project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2026.03.0002] - 2026-03-16

### Added
- **PowerShell Gallery Publishing**: Script available via `Install-Script universal-intel-wifi-bt-driver-updater`
- **Multi-Database Support**: `-beta` flag uses `intel-wifi-driver-beta.md` / `intel-bt-driver-beta.md`; `-developer` flag uses dev databases; default behavior unchanged (stable `*-latest.md`)
- **Dynamic Support Message**: Credits screen loads support message from GitHub (`data/intel-wifi-bt-message.txt`) at runtime with inline color tag support; falls back to built-in static version if GitHub is unreachable
- **Help System Unified**: `-help` and `-?` now show identical output via native `Get-Help`
- **Improved Console Exit**: When launched from a PowerShell console (not SFX), screen is cleared after credits and a clean thank-you message is displayed before returning to the prompt

### Changed
- **Architecture Rebuilt — BAT Launcher Retired**: `Universal-Intel-WiFi-BT-Updater.bat` removed from the release; the script now auto-elevates natively; tool distributed exclusively as PS1 (for administrators) or SFX EXE (for end users)
- **Script Renamed**: From `Universal-Intel-WiFi-BT-Updater.ps1` to `universal-intel-wifi-bt-driver-updater.ps1` to align with PSGallery naming convention
- **Path Handling**: Replaced hardcoded `C:\Windows\Temp` and `C:\ProgramData` with `$env:SystemRoot` and `$env:ProgramData` for compatibility with non-standard Windows installations
- **Auto Mode Cleanup**: Removed unnecessary wait at the end of `-auto` / `-quiet` runs — script exits immediately after completion

### Technical Improvements
- **Boolean Flags**: Refactored `$DebugMode` and `$SkipSelfHashVerification` from integer `0`/`1` flags to native PowerShell `[bool]` types
- **Dual Independent Detection**: Wi-Fi (PCI bus, VEN_8086) and Bluetooth (USB bus, VID_8087) detected and installed independently
- **Bluetooth Device Fallback**: BT detection attempts `Bluetooth` device class first, then falls back to full USB bus scan (`VID_8087`)
- **Version Comparison**: Replaced string comparison with `[version]` cast for correct multi-part driver version handling
- **Code Cleanup**: Removed redundant wrapper functions — logic inlined directly into core verification routines
- **Consistency**: Replaced all `cls` alias occurrences with `Clear-Host`
- **Logging**: All actions written to `%ProgramData%\wifi_bt_update.log` with timestamps and severity levels

### Security
- **Maintained Integrity Checks**: Self-hash SHA-256 verification and Intel Authenticode digital signature validation remain intact
- **Secure Temporary File Handling**: Automatic cleanup of all temporary files after completion

---

## [v24.0 (2025.11)] - 2025-11-xx — Legacy Release

### Added
- **Initial Public Release** of Universal Intel Wi-Fi and Bluetooth Drivers Updater
- **Automatic Hardware Detection**: Scans for Intel Wi-Fi and Bluetooth adapters
- **Wi-Fi and Bluetooth Support**: Wi-Fi 5 (AC) / Wi-Fi 6 (AX) / Wi-Fi 6E (AXE) / Wi-Fi 7 (BE) and Bluetooth
- **Dual-Script Architecture**: BAT launcher (`Universal-Intel-WiFi-BT-Updater.bat`) for UAC elevation + PowerShell script for core functionality
- **SHA-256 Hash Verification**: Every downloaded CAB package validated before installation
- **System Restore Point Creation**: Automatic restore point before any driver changes
- **Digital Signature Validation**: Verification of Intel Authenticode certificates

### Security
- **Multi-layer Verification**: SHA-256 hash checks + Intel digital signature validation
- **Administrator Rights Required**: Mandatory elevation via BAT launcher for system-level operations
- **Dual-Source Download**: Primary and backup download sources for reliability

---

## Release Notes Format

### Version Naming Convention
- **YYYY.MM.REVISION** format (e.g., `2026.03.0002`)
- Date component reflects release year and month
- Revision number increments with each update

### Categories Used
- **Added**: New features and capabilities
- **Changed**: Modifications to existing functionality
- **Fixed**: Bug fixes and issue resolutions
- **Security**: Security-related improvements and fixes
- **Deprecated**: Features marked for future removal (if applicable)
- **Removed**: Features removed in this version (if applicable)

---

## Links

- [Latest Release](https://github.com/FirstEverTech/Universal-Intel-WiFi-BT-Updater/releases/latest)
- [All Releases](https://github.com/FirstEverTech/Universal-Intel-WiFi-BT-Updater/releases)
- [Issue Tracker](https://github.com/FirstEverTech/Universal-Intel-WiFi-BT-Updater/issues)
- [Security Policy](https://github.com/FirstEverTech/Universal-Intel-WiFi-BT-Updater/blob/main/SECURITY.md)

---

## Support

If you encounter any issues or have questions about a specific release:
1. Check [Known Issues](https://github.com/FirstEverTech/Universal-Intel-WiFi-BT-Updater/blob/main/KNOWN_ISSUES.md)
2. Search [Existing Issues](https://github.com/FirstEverTech/Universal-Intel-WiFi-BT-Updater/issues)
3. Create a [New Issue](https://github.com/FirstEverTech/Universal-Intel-WiFi-BT-Updater/issues/new) with detailed information

---

**Note**: This project is independent and not affiliated with Intel Corporation. All driver packages are official Intel releases downloaded from Intel's servers.
