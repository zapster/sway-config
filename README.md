# Sway configuration

Sway with Alacritty, Rofi, and Waybar using Hack Nerd Font.

## Dependencies

| Tools/services | Purpose |
| --- | --- |
| Sway (`sway`, `swaymsg`, `swaynag`), `swaybg` | Compositor, session controls, wallpaper |
| `alacritty`, `rofi` (2.0+ with Wayland support) | Terminal and launcher |
| `waybar`, Hack Nerd Font | Bar and icons |
| PipeWire, pipewire-pulseaudio, WirePlumber (`wpctl`) | Audio widgets and media keys |
| `brightnessctl`, supported kernel backlight | Brightness keys |
| `pavucontrol`, `nm-connection-editor`, NetworkManager | Bar settings actions |
| `grim`, `slurp`, `swappy` | Screen/area capture and editing, save/copy |
| `xdg-desktop-portal`, `xdg-desktop-portal-wlr`, `xdg-desktop-portal-gtk` | Screen sharing and desktop integration |
| `swaylock`, `swayidle` | Screen locking, idle timers, pre-suspend locking |
| `dbus-update-activation-environment` (dbus-tools), systemd/logind (`loginctl`) | Session environment and lock/suspend integration |

## Setup

Clone to `~/.config/sway` and link the Waybar configuration:

```bash
ln -s ~/.config/sway/waybar ~/.config/waybar
```

Install the screenshot launchers and link Swappy settings:

```bash
mkdir -p ~/.local/share/applications ~/.config/swappy
for mode in area screen; do
    sed "s|@SCRIPT@|$HOME/.config/sway/scripts/screenshot|g" \
        ~/.config/sway/applications/sway-screenshot-$mode.desktop.in \
        > ~/.local/share/applications/sway-screenshot-$mode.desktop
done
ln -s ~/.config/sway/swappy/config ~/.config/swappy/config
```

**Screenshot Area/Screen** in Rofi opens Swappy: Ctrl+C copies; Ctrl+S saves to
`~/Pictures/Screenshots` with a timestamped name. Copy or save closes the window;
close without either to discard. Ctrl+B toggles the hidden editing panel.

For the existing **Sway with Keyring** GDM entry, install the session wrapper:

```bash
sudo install -m 755 ~/.config/sway/scripts/session /usr/local/bin/sway-session
```

Machine-specific startup settings go in ignored `session.local`.

Validate with `sway --validate --config ~/.config/sway/config`.
Reload with **Super+Shift+C**.

**Super+D** searches applications and PATH commands in one Rofi menu.

**Ctrl+Alt+L** locks. Idle locking starts after 5 minutes; displays turn off after
10 minutes and wake on input. Locking also runs before suspend. Lid behavior
uses logind defaults; no automatic idle-suspend timer is configured.
Restart `swayidle` after editing `idle.conf`; ordinary Sway reloads keep it running.

Volume keys use 5% steps; brightness keys use 10%. Volume increases stop at 100%.
Untouched system configuration baseline: `80785d4`.
