# Windows native layout installer

This prebuilt bundle installs **LTS (US)** as a native Windows keyboard layout for English (United States). MSKLC is only needed to [build from source](../source/README.md), not to install the bundled package.

**Installation and uninstallation have been tested on Windows 11 x64.** Other Windows versions and architectures have not been verified for this package.

## Install the prebuilt layout

1. Download this repository using **Code → Download ZIP** and extract it to a local folder.
2. Open `windows/installer/` and run [`setup.exe`](setup.exe). Keep the MSI files and architecture directories alongside it, with their names and relative paths unchanged. **Do not download or copy `setup.exe` alone**, and do not copy DLLs into Windows system folders manually.
3. Follow the installer prompts and approve administrator access. Only run a package from a source you trust.
4. Stop any AutoHotkey/Kanata remapper before selecting native LTS. Do not stack it with keyboard firmware that already outputs LTS.
5. Sign out/in if necessary. In **Settings → Time & language → Language & region → English (United States) → Language options → Keyboards**, add/select **LTS (US)**. Windows versions may use slightly different labels. Keep **US** installed for recovery and use **Win+Space** to switch layouts.

Keep the complete installer bundle until removal has been verified. For typing and shortcut checks, see the [behavior and verification checklist](../source/README.md#behavior-and-verification).

## Architecture notes

Use `setup.exe` as the normal installation entry point. The generated bundle contains:

| Files                     | Architecture                                | Verification                                             |
| ------------------------- | ------------------------------------------- | -------------------------------------------------------- |
| `lts_amd64.msi`, `amd64/` | x64 (Intel or AMD)                          | Installation and uninstallation tested on Windows 11 x64 |
| `lts_i386.msi`, `i386/`   | 32-bit x86                                  | Included, unverified                                     |
| `lts_ia64.msi`, `ia64/`   | Legacy Itanium (IA64), **not ARM64**        | Included, unverified                                     |
| `wow64/`                  | 32-bit compatibility DLL for 64-bit Windows | Supporting files, not a separate installer               |

There is **no native ARM64 package** in this bundle. Do not assume these packages work on Windows on ARM. [AutoHotkey v2](../../autohotkey/README.md) and [Kanata](../../kanata/README.md) are alternative implementations; check their platform and architecture support separately.

## Remove

Switch to **US** first, remove LTS from your language's keyboard list, then uninstall **LTS (US)** through Windows' installed-apps/programs settings or the matching setup package's removal option. Sign out/in if needed. Keep the complete installer bundle until removal has been verified.
