# Linux desktop: XKB

[`symbols/lts`](symbols/lts) defines layout `lts`, variant `basic`, based on `us(basic)`. It explicitly distinguishes alphabetic and punctuation key types so Caps Lock affects letters, not punctuation.

The commands below run from the repository root. **Do not run Kanata or another layout remapper at the same time.** Keep US available for recovery. Console/TTY configuration is [separate](../console/README.md).

## Validate without changing your layout

Install your distribution's libxkbcommon tools and xkeyboard-config data (sometimes named `libxkbcommon-tools` and `xkb-data`):

```sh
xkbcli compile-keymap --include "$PWD/linux/xkb" --include-defaults --layout lts --variant basic --test
```

The include-defaults option retains the system's standard XKB types, keycodes, and US symbols. Validation does not activate the layout.

## Wayland: user-local installation

On setups using libxkbcommon's user configuration paths:

```sh
mkdir -p "${XDG_CONFIG_HOME:-$HOME/.config}/xkb/symbols"
cp linux/xkb/symbols/lts "${XDG_CONFIG_HOME:-$HOME/.config}/xkb/symbols/lts"
```

If that destination already exists, inspect/back it up before replacing it.

Select layout `lts` and variant `basic` in your compositor configuration.

For GNOME/KDE or other graphical selectors, [`rules/evdev.xml`](rules/evdev.xml) supplies the layout's discovery metadata:

1. Create `${XDG_CONFIG_HOME:-$HOME/.config}/xkb/rules`.
2. If it has **no** `evdev.xml`, copy this repository's `linux/xkb/rules/evdev.xml` there.
3. If an `evdev.xml` already exists, merge just the `<layout>` entry into its `<layoutList>`; **do not overwrite other custom layouts**.
4. Log out/in if necessary, then add **LTS (US)** using your desktop's keyboard/input-source settings.

User-local discovery requires a selector using libxkbregistry. Some desktop versions ignore user-local registry files; use the desktop's supported custom-layout mechanism or a system-managed installation instead. `setxkbmap` does **not** configure a Wayland compositor.

## X11: try without installing system files

With `setxkbmap` and `xkbcomp` installed, compile the local symbols and send the complete keymap to the X server:

```sh
setxkbmap -I"$PWD/linux/xkb" -layout lts -variant basic -print |
    xkbcomp -I"$PWD/linux/xkb" - "$DISPLAY"
```

This affects the current X11 session. Restore US with:

```sh
setxkbmap -layout us -variant ''
```

For persistence, configure your session to run the activation command with an absolute include path, or register the layout using your distribution's system configuration. X servers do not generally use libxkbcommon's user-local lookup paths; copying into `~/.config/xkb` alone is not sufficient for X11.

## System-managed installations and NixOS

Avoid editing packaged `us`, `evdev`, or `base` files: updates can overwrite those changes. Install this as an additional layout using your distribution's supported packaging/configuration mechanism. On NixOS, declare an extra XKB layout with this symbols file and select `lts` in the relevant desktop/compositor configuration; do not edit `/nix/store` or symlinked packaged XKB data. Apply any system configuration changes yourself.

See [libxkbcommon's custom configuration guide](https://xkbcommon.org/doc/current/custom-configuration.html) for lookup paths and desktop discovery limitations.

## Remove

Switch to US first and remove LTS from your desktop/compositor configuration and any autostart command. Delete only the copied `symbols/lts` file and the LTS registry entry. If the registry file contains other customizations, preserve them. A session restart may be needed.
