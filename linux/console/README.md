# Linux console / TTY

[`lts.map`](lts.map) is a complete console map built on the standard `kbd` US includes. It preserves the US function keys, keypad, navigation, and remaining punctuation, and remaps every modifier column on the 30 typing keys. Ctrl-letter combinations follow LTS; Caps Lock applies only to letters.

This is for **Linux virtual consoles**, not graphical terminal applications. A terminal inside GNOME, KDE, Sway, etc. uses the desktop's [XKB layout](../xkb/README.md) instead. If Kanata already remaps your console input, do not load LTS here as well.

## Validate without loading

Install your distribution's `kbd` tools **and keymap data**, including the standard `linux-with-alt-and-altgr`, `compose.latin1`, and `euro1.map` includes. From the repository root:

```sh
loadkeys --mktable linux/console/lts.map > /dev/null
```

`--mktable` compiles to C on stdout; it does not change a console or require root.

## Try and recover

1. Switch to a virtual console
2. From the repository root, apply LTS:

   ```sh
   sudo loadkeys linux/console/lts.map
   ```

3. To restore US:

   ```sh
   sudo loadkeys us
   ```

If typing the recovery command is difficult, use the other session or reboot without making LTS persistent.

## Persistence and removal

On a conventional systemd distribution, copy the map into the distribution's local console-keymap directory (commonly `/usr/local/share/kbd/keymaps/`, but lookup paths vary), then set `KEYMAP` in `/etc/vconsole.conf` to the installed map's **absolute path**. Preserve other settings and record your previous `KEYMAP`. Consult your distribution's instructions; some use a different configuration system.

On NixOS/other immutable systems, reference the map through the declarative console configuration rather than writing into packaged data directories. Apply system changes yourself. Early-boot disk-unlock prompts may need a separate initramfs rebuild; do not assume they use LTS. Keep the previous layout available.

To remove, restore the previous persistent console configuration, load the old map (or reboot), and delete only the LTS map you installed.
