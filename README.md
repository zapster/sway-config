# Sway and Waybar configuration

This repository lives at `~/.config/sway`. Its first commit, `80785d4`, contains
an exact copy of `/etc/sway/config` before customization. Git identity is set
locally to Josef Eisl <zapster@zapster.cc>.

## Files

- `config`: full Sway configuration, including the existing D-Bus/systemd session
  environment publication and Alacritty on Super+Enter.
- `assets/sway-background.png`: wallpaper copied from the sway background package
  at `/usr/share/backgrounds/sway/Sway_Wallpaper_Blue_1920x1080.png`.
- `waybar/config.jsonc` and `waybar/style.css`: top bar prepared from the accepted
  demo, without its demo label. `~/.config/waybar` links to this directory.

The configuration does not include `/etc/sway/config` or its `config.d` directory
(the latter was empty when migrated). Installed applications, fonts, and system
services remain dependencies. Review system Sway updates against the baseline
before selectively adopting their configuration changes.

## Waybar activation pending

Waybar is not yet installed. The default Swaybar remains configured so the next
login or reload still has a bar. The separate demo may continue running until
Waybar is installed and permanent activation is completed.

Once `/usr/bin/waybar` is installed, replace the existing `bar` block with:

```text
bar {
    swaybar_command waybar
}
```

Validate with `sway --validate --config ~/.config/sway/config`, stop the
`laptop-waybar-demo.service` user unit, and reload Sway. Commit the activation
separately. Do not add a second autostart command or a separate Waybar service.

## Controls and dependencies

- Network right-click: `nm-connection-editor`; no network applet.
- Volume scroll: adjust volume. Left-click: mute using `wpctl`.
  Right-click: open `pavucontrol`.
- Clock: explicit 24-hour `%H:%M` format.
- Font: installed Hack Nerd Font.
- Tray: icons supplied by compatible running applications.

The inherited media/brightness key bindings still reference `pactl` and
`brightnessctl`; migration of those controls remains pending in the laptop setup
TODO. The launcher remains `wmenu-run` pending a separate decision.

## Recovery

The first commit is the untouched system configuration. Use `git log` and
`git diff` to review changes, and `git restore --source=<commit> -- config` to
restore a chosen version before validation and reload. Restoring the first
commit also restores its system dependencies and default terminal/bar choices.

The pre-migration include-based config was backed up under
`~/.local/state/laptop-setup/20261106-123456-standalone-sway/sway-config`.
