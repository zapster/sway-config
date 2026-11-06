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
| `dbus-update-activation-environment` (dbus-tools), systemd user session | Session environment |

The commented idle/lock example additionally requires `swayidle` and `swaylock`.

## Setup

Clone to `~/.config/sway` and link the Waybar configuration:

```bash
ln -s ~/.config/sway/waybar ~/.config/waybar
```

Validate with `sway --validate --config ~/.config/sway/config`.
Reload with **Super+Shift+C**.

Media and brightness keys use 5% steps; volume increases stop at 100%.
Untouched system configuration baseline: `80785d4`.
