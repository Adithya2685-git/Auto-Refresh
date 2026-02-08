# Refresh Rate & Power Switcher

Signal-based auto-switching for display refresh rate and system power profile based on power source.

## Features
- **Signal-based**: Uses D-Bus signals for instant power state detection (no polling)
- **Refresh Rate**: 240Hz (AC) ↔ 60Hz (Battery)
- **Power Profile**: Performance (AC) ↔ Power-saver (Battery)
- **Graceful shutdown**: Handles SIGINT/SIGTERM
- **Auto-start**: systemd user service

## Installation

```bash
cd ~/refresh-switch
cargo build --release
cp target/release/refresh-switch ~/.local/bin/
systemctl --user daemon-reload
systemctl --user enable refresh-switch.service
```

## Usage

```bash
# Start now
systemctl --user start refresh-switch.service

# Check status
systemctl --user status refresh-switch.service

# View logs
journalctl --user -u refresh-switch.service -f
```

## Dependencies
- hyprland + hyprctl
- power-profiles-daemon (powerprofilesctl)
- UPower (D-Bus)
- systemd
