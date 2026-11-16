# AutoHotkey v2 (Windows)

[`lts.ahk`](lts.ahk) is a lightweight trial option. It needs **AutoHotkey v2**, not v1, and a normal **US QWERTY** Windows input source.

## Run

1. Install [AutoHotkey v2](https://www.autohotkey.com/).
2. Double-click `lts.ahk`.

## Stop and remove

Right-click the script's tray icon and choose **Exit** to restore normal input. Release held keys before exiting. **Suspend Hotkeys** in the tray menu can temporarily disable remapping.

Optionally add a shortcut to the script in your Windows startup folder (`Win+R` → `shell:startup`). To remove, delete that shortcut, exit the running script, and delete the script file. Nothing is written to the keyboard-layout registry by this script.

## Limitations

- AutoHotkey must keep running. It is not a native installed Windows layout.
- Elevated applications may reject input from a non-elevated script. Run at matching privilege only when necessary; prefer [native LTS](../windows/installer/README.md) if this is an ongoing problem.
- Secure desktop/UAC/logon screens and applications using raw input may not use the remapping.
- Switching Windows input sources away from US can change results. Do not stack this with Kanata, native LTS, or firmware that already produces LTS.
