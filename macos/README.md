# macOS native layout

[`LTS.keylayout`](LTS.keylayout) is an installable macOS input source named **LTS**. It does not need Kanata, a keyboard driver, or a background process. This is the US baseline, not a separate ISO/UK/JIS localization.

## Install

From the extracted repository root:

```sh
mkdir -p "$HOME/Library/Keyboard Layouts"
cp macos/LTS.keylayout "$HOME/Library/Keyboard Layouts/LTS.keylayout"
```

Log out/in if the input source is not immediately visible. Open **System Settings → Keyboard → Text Input → Edit → +**, find **LTS** (it may appear under **Others**), and add it. Enable the input menu and keep US or ABC available for recovery. Older macOS versions use **System Preferences → Keyboard → Input Sources**.

## Behavior and testing

- Command-letter shortcuts follow LTS, including Command+C at physical QWERTY `V`.
- Shift and Caps Lock affect letters; punctuation retains its normal US shifted partner.
- Option symbols follow the logical US letters: for example, Option+C gives `ç` at the LTS `C` position. The usual US accent dead keys (Option+E/I/U/N/grave) are provided. Other US keys keep their usual base/Shift/Option outputs.
- Ctrl-letter outputs follow LTS for terminal use.
- Numbers, brackets, quotes, backslash, grave, keypad, navigation, and function keys retain the US baseline behavior.

The file uses Apple's XML 1.1 keylayout format (including numeric references for nonprinting control characters). Check Command+C/V/Z/A, Caps Lock, Shift+Caps Lock, and Option accents. [Ukelele](https://software.sil.org/ukelele/) can inspect the layout without hand-editing XML.

## Remove

Switch to other layout first. Remove LTS from the input-source list, delete only `~/Library/Keyboard Layouts/LTS.keylayout`, and log out/in if necessary. No daemon or driver needs uninstalling.
