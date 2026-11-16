# Windows layout source

[`lts.klc`](lts.klc) is a **Microsoft Keyboard Layout Creator (MSKLC) source file**, encoded as UTF-16LE with a BOM and Windows line endings. It describes **LTS (US)** for English (United States). A `.klc` cannot be installed by copying it into a Windows system folder.

To use the prebuilt package without MSKLC, follow the [installer guide](../installer/README.md).

## Build from source

1. Install [Microsoft Keyboard Layout Creator 1.4](https://www.microsoft.com/en-us/download/details.aspx?id=102134) and the .NET prerequisites its installer requires. MSKLC is an older tool; check its current compatibility with your Windows version.
2. Copy `windows/source/lts.klc` from the extracted repository to a simple local path such as `C:\LTS\lts.klc`.
3. Open MSKLC, then **File → Load Source File** and choose `lts.klc`.
4. Verify the base and Shift mappings. Run **Project → Validate Layout**, inspect any warnings, and use **Project → Test Keyboard Layout** where available.
5. Choose **Project → Build DLL and Setup Package**. Select a writable output directory separate from the bundled installer, for example `C:\LTS\build`.
6. Run the newly generated `setup.exe` with its own complete bundle. Follow the [installation and removal instructions](../installer/README.md), using your newly generated package rather than the repository's prebuilt files. Test your rebuilt package separately; the bundled package's test status does not verify a rebuild.

## Build naming and virtual keys

The source declares internal name `lts_us`, while the bundled package uses `lts.dll` and `lts_*.msi`. Do not assume rebuilding the unchanged source will reproduce the bundled filenames. If maintaining the `lts` package name, align the MSKLC project's internal name before building. Do not rename generated files manually or mix files from separate builds.

Virtual-key assignments in the source follow **LTS letters**, not the original QWERTY positions. This is essential for Ctrl/Alt/Windows-letter shortcuts. Do not replace the virtual-key column with physical QWERTY letters when editing or rebuilding.

## Behavior and verification

- All rows, Shift, Caps Lock, and Shift+Caps Lock (especially letters moved onto punctuation keys).
- Ctrl+C, Ctrl+V, Ctrl+Z, Ctrl+A, Alt-letter shortcuts, and terminal Ctrl-letter behavior.
- Unchanged numbers, brackets, quote, backslash, grave, keypad, modifiers, navigation, and function keys.
- Installation, input-source switching, sign-out/in, and uninstall on each advertised Windows version/architecture.
