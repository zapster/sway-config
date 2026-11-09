# Sway configuration

Sway with Alacritty, wmenu, and Waybar using Hack Nerd Font.

## Dependencies

| Tools/services | Purpose |
| --- | --- |
| Sway (`sway`, `swaymsg`, `swaynag`), `swaybg` | Compositor, session controls, wallpaper |
| `alacritty`, `wmenu-run` (wmenu) | Terminal and launcher |
| `waybar`, Hack Nerd Font | Bar and icons |
| PipeWire, pipewire-pulseaudio, WirePlumber (`wpctl`) | Audio widgets and media keys |
| `brightnessctl`, supported kernel backlight | Brightness keys |
| `pavucontrol`, `nm-connection-editor`, NetworkManager | Bar settings actions |
| `grim` | Print-key screenshots |
| `swaylock`, `swayidle` | Screen locking, idle timers, pre-suspend locking |
| `dbus-update-activation-environment` (dbus-tools), systemd/logind (`loginctl`) | Session environment and lock/suspend integration |

## Setup

Clone to `~/.config/sway` and link the Waybar configuration:

```bash
ln -s ~/.config/sway/waybar ~/.config/waybar
```

Validate with `sway --validate --config ~/.config/sway/config`.
Reload with **Super+Shift+C**.

**Ctrl+Alt+L** locks. Idle locking starts after 5 minutes; displays turn off after
10 minutes and wake on input. Locking also runs before suspend. Lid behavior
uses logind defaults; no automatic idle-suspend timer is configured.
Restart `swayidle` after editing `idle.conf`; ordinary Sway reloads keep it running.

Volume keys use 5% steps; brightness keys use 10%. Volume increases stop at 100%.
Untouched system configuration baseline: `80785d4`.
