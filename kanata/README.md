# Kanata

[`lts.kbd`](lts.kbd) remaps the 30 US-QWERTY typing positions. Unlisted keys pass through unchanged. Shift, Caps Lock, Ctrl, Alt, and Command/Windows/Super use the remapped letters; no extra layers or modifier tricks are added.

## Install and try

1. Install [Kanata](https://github.com/jtroo/kanata/releases) for your platform. Follow its release-specific setup instructions.
2. Select the normal **US QWERTY** OS input source (US or ABC on macOS). Disable other layout remappers, including keyboard firmware that already outputs LTS.
3. Start it in the foreground, then test in an empty text editor:

   **Linux:** with the input-device/uinput permissions described by Kanata, run:

   ```sh
   kanata --cfg kanata/lts.kbd
   ```

   For a temporary test, Kanata also documents running this with `sudo`. Prefer its [non-root setup](https://github.com/jtroo/kanata/wiki/Avoid-using-sudo-on-Linux) for regular use. This backend works below X11/Wayland and can also affect TTYs while running; do not load the console LTS map on top of it.

   **Windows (PowerShell):** from the extracted repository, using your downloaded binary's actual path:

   ```powershell
   C:\path\to\kanata.exe --cfg .\kanata\lts.kbd
   ```

   Elevated applications may require Kanata to run at matching privilege. Do not elevate unless needed. The Windows hook backend cannot remap every secure/system context; consult [known issues](https://github.com/jtroo/kanata/blob/main/docs/platform-known-issues.adoc).

   **macOS:** install the driver required by your Kanata release and grant the documented input permissions first. Follow [Kanata's macOS instructions](https://github.com/jtroo/kanata#build-it-yourself); Native [LTS.keylayout](../macos/) avoids this remapping driver entirely.

Keep the foreground process open while using LTS. The same config works across the three platforms, but installing Kanata and granting permissions is platform-specific.

## Stop, persist, remove

- Stop the foreground process to restore US QWERTY.
- Configure autostart using Kanata's platform-specific instructions and an **absolute** path to this config. This repository does not enable services or autostart automatically.
- To remove: disable any autostart you added, stop Kanata, and remove the copied config. Uninstall Kanata/its driver separately if no longer needed.
