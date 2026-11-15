# Windows native layout

[`lts.klc`](lts.klc) is a **Microsoft Keyboard Layout Creator (MSKLC) source file**, encoded as UTF-16LE with a BOM and Windows line endings. It describes **LTS (US)**, internal name `lts_us`, English (United States).

**No prebuilt `.exe`/`.msi` installer is included yet.** A `.klc` cannot be installed by copying it into a Windows system folder. Build the native installer on Windows, or use [AutoHotkey v2](../autohotkey/README.md) / [Kanata](../kanata/README.md) to try LTS immediately.

## Build and install on Windows

1. Install [Microsoft Keyboard Layout Creator 1.4](https://www.microsoft.com/en-us/download/details.aspx?id=102134) and the .NET prerequisites its installer requires. MSKLC is an older tool; check its current compatibility with your Windows version.
2. Copy `lts.klc` to a simple local path such as `C:\LTS\lts.klc`.
3. Open MSKLC, then **File → Load Source File** and choose `lts.klc`.
4. Verify the base and Shift mappings. Run **Project → Validate Layout**, inspect any warnings, and use **Project → Test Keyboard Layout** where available.
5. Choose **Project → Build DLL and Setup Package**. Select a writable output directory, for example `C:\LTS\build`.
6. Run the generated `setup.exe`, following its prompts. This installs a system keyboard layout and requires administrator approval. Use only the package built from this source or a trusted future release.
7. Sign out/in if necessary. In **Settings → Time & language → Language & region → English (United States) → Language options → Keyboards**, add/select **LTS (US)**. Windows versions may use slightly different labels. Keep US installed and use **Win+Space** to switch.
8. Stop any AHK/Kanata remapper before selecting native LTS.

Virtual-key assignments in the source follow **LTS letters**, not the original QWERTY positions. This is essential for Ctrl/Alt/Windows-letter shortcuts. Do not replace the virtual-key column with physical QWERTY letters when editing or rebuilding.

## Test before distributing installers

MSKLC compilation and interactive Windows behavior still require platform testing. Before distributing a package, verify:

- All rows, Shift, Caps Lock, and Shift+Caps Lock (especially letters moved onto punctuation keys).
- Ctrl+C, Ctrl+V, Ctrl+Z, Ctrl+A, Alt-letter shortcuts, and terminal Ctrl-letter behavior.
- Unchanged numbers, brackets, quote, backslash, grave, keypad, modifiers, navigation, and function keys.
- Installation, input-source switching, sign-out/in, and uninstall on each advertised Windows version/architecture.

Do not assume MSKLC produces a usable native ARM64 package. Use a tested remapper on architectures not verified with the native installer. Publish only platform-built, tested installer files.

## Remove

Switch to **US** first, remove LTS from your language's keyboard list, then uninstall **LTS (US)** through Windows' installed-apps/programs settings or the generated setup package's removal option. Sign out/in if needed. Keep the generated package until removal has been verified.
