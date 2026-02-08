# Agent Context - System Configuration

This document contains essential context for AI coding agents working with this user's system.

## System Information

- **OS**: CachyOS (Arch-based)
- **Desktop Environment**: Hyprland (Wayland compositor)
- **Shell**: Fish
- **Terminal**: Kitty
- **Text Editor**: **micro** (PREFERRED - DO NOT use nano)
- **Package Manager**: pacman, paru (AUR helper)
- **Laptop**: ASUS (uses asusctl for hardware control)
- **Graphics**: Hybrid Intel + NVIDIA

## Critical Rules

### NEVER DO THESE:
1. **NEVER create bash scripts** - Update config files directly instead
2. **NEVER use nano** - User prefers micro
3. **NEVER add auto-suspend** - User removed it intentionally
4. **NEVER use wofi** - User uses hyprlauncher (wofi should be uninstalled)
5. **NEVER create unnecessary files** - Only edit existing configs

### Always Do:
1. Use config files directly when possible
2. Ask before making major changes
3. Test commands before adding to config
4. Keep things minimal and clean

## Hyprland Setup

### Installed Ecosystem Packages
- hyprland - Window manager
- waybar - Status bar (floating pill minimalist style, replaced hyprpanel)
- hyprlauncher - Application launcher
- hyprlock - Screen locker
- hypridle - Idle daemon
- hyprpaper - Wallpaper manager
- hyprpicker - Color picker
- hyprshot - Screenshot tool
- hyprsunset - Blue light filter
- hyprshutdown - Graceful shutdown GUI (AUR)
- hyprpwcenter - PipeWire control center (replaces pavucontrol)
- hyprpolkitagent - Polkit authentication agent
- hyprland-qt-support - QML style provider for Hypr QT apps
- hyprtoolkit - C++ Wayland-native GUI toolkit
- hyprcursor - Cursor format/library
- hyprutils - Utility library
- hyprlang - Config language parser
- hyprwayland-scanner - Wayland protocol scanner
- hyprgraphics - Graphics library
- hyprland-guiutils - GUI utilities
- hyprwire - Network management
- aquamarine - Wayland backend
- xdg-desktop-portal-hyprland - XDG portal
- cliphist - Clipboard manager
- grim + slurp - Screenshot utilities
- brightnessctl - Brightness control
- gnome-keyring - Secret service for apps (Mailspring etc.)
- NOT AVAILABLE YET: hyprsysteminfo, hyprqt6engine

### Configuration Locations
- Main config: `~/.config/hypr/hyprland.conf`
- Lock screen: `~/.config/hypr/hyprlock.conf`
- Idle config: `~/.config/hypr/hypridle.conf`
- Wallpaper: `~/.config/hypr/hyprpaper.conf`
- Panel config: `~/.config/waybar/config.jsonc`
- Panel style: `~/.config/waybar/style.css`
- Terminal: `~/.config/kitty/kitty.conf`

### Keybindings
```
# System
SUPER + Q = Terminal (kitty)
SUPER + R = Launcher (hyprlauncher)
SUPER + E = File manager (nautilus)
SUPER + C = Close window
SUPER + M = Exit Hyprland
SUPER + V = Toggle floating
SUPER + L = Lock screen (hyprlock)
SUPER + B = Firefox
SUPER + SHIFT + B = Firefox private window

SUPER + F = Fullscreen toggle

# Screenshots
Print = Full screen screenshot
SUPER + Print = Window screenshot
SUPER + SHIFT + Print = Region screenshot

# Utilities
SUPER + X = Clipboard history (with hyprlauncher)
SUPER + N = Toggle blue light filter (hyprsunset)
F7 = Brightness down
F8 = Brightness up

# Workspaces
SUPER + [1-9,0] = Switch workspace
SUPER + SHIFT + [1-9,0] = Move window to workspace
SUPER + Arrow keys = Move focus

# Audio/Media
Fn + Volume keys = Volume control (wpctl)
Fn + Media keys = Media controls (playerctl)
```

### Theme: Pitch Black
- Background: Pure black (#000000)
- Text: White (#ffffff)
- Borders: Subtle white (#333333, #666666)
- Active elements: White with transparency
- Panel: Floating pill modules, transparent bg, dark opaque modules
- No colorful accents - minimalistic monochrome
- Wallpaper: Subtle radial gradient (dark gray center to black edges) at 2560x1600

### Panel Configuration (Waybar)
- Height: 40px
- Position: Top
- Style: Floating pill-shaped modules (transparent panel bg, opaque #000 module bg)
- Layout: `[workspaces dots] [center:clock] [tray audio battery session]`
- Workspaces: 5 pinned, dot indicators (small circles)
- Tray: nm-applet (WiFi) + blueman-applet (Bluetooth) icons with native menus
- Audio: Nerd font icon, left-click opens hyprpwcenter
- Battery: Nerd font icon with charging/warning states
- Session: Power icon, left-click opens hyprshutdown
- No taskbar, no date display
- Monochrome: white icons/text on #000 pill backgrounds

### Autostart Services
```bash
exec-once = dbus-update-activation-environment --systemd WAYLAND_DISPLAY XDG_CURRENT_DESKTOP
exec-once = systemctl --user import-environment WAYLAND_DISPLAY XDG_CURRENT_DESKTOP
exec-once = /usr/lib/hyprpolkitagent/hyprpolkitagent
exec-once = gnome-keyring-daemon --start --components=secrets
exec-once = hyprpaper
exec-once = waybar
exec-once = nm-applet --indicator
exec-once = blueman-applet
exec-once = hypridle
exec-once = hyprlauncher -d
exec-once = wl-paste --watch cliphist store
```

### Idle Behavior
- 5 min: Dim brightness to 10%
- 10 min: Lock screen
- 15 min: Turn off display
- NO auto-suspend (user removed it)

## Hardware Control

### Brightness
- Uses: `brightnessctl -d intel_backlight`
- Device: `/sys/class/backlight/intel_backlight/`
- Bindings use F7/F8 keys
- Step: 5%

### Graphics
- Primary display: Intel iGPU
- NVIDIA: For gaming/heavy tasks
- Uses PRIME render offload for games
- Check with: `supergfxctl -g` (if installed)

### ASUS-specific
- Keyboard backlight: `asusctl leds`
- Don't use asusctl for screen brightness

## Package Management

### Installing Packages
```bash
# Official repos
sudo pacman -S package-name

# AUR
paru -S package-name

# Check if installed
pacman -Qq | grep package-name
```

### Common Packages
- brightnessctl (for brightness)
- wl-clipboard (for clipboard)
- grim + slurp (for screenshots)
- playerctl (for media keys)

## File Operations

### Editor Preference
- **USE**: micro
- **NEVER USE**: nano, vi, vim (unless specifically requested)

### Config File Editing
1. Always read the file first
2. Use the Edit tool to modify specific sections
3. Reload services after changes:
   - Hyprland: `hyprctl reload`
   - Panel: `pkill waybar && waybar &`
   - Wallpaper: `pkill hyprpaper && hyprpaper &`

## Communication Style

### User Preferences
- Be direct and concise
- Don't create unnecessary files
- Don't write bash scripts unless absolutely necessary
- Just update config files
- Test before implementing
- Strong language is acceptable when correcting mistakes

### Problem Solving
1. Check if tool/package is installed first
2. Read existing configs before modifying
3. Use native Hyprland features when possible
4. Keep solutions minimal
5. Don't over-engineer

## Recent Changes History

### Theme Changes
- Changed from default blue/cyan theme to pitch black
- Updated all colors in hyprland.conf and waybar style.css
- Borders: white with low opacity
- Shadows: pure black

### Panel Changes
- Switched from HyprPanel to Waybar (HyprPanel had broken systray menus)
- Floating pill-shaped modules (transparent panel, opaque #000 module backgrounds)
- Workspace dots (small circles, not rectangles)
- Only 5 pinned workspaces
- Tray: nm-applet + blueman-applet with working native dropdown menus
- Audio widget opens hyprpwcenter (native Hypr PipeWire center)
- Session widget opens hyprshutdown (native Hypr graceful shutdown GUI)
- Battery widget with nerd font icons
- Removed taskbar (no app icons)
- Removed date from clock
- Notifications: need a notification daemon (mako was removed, HyprPanel used to handle this)

### Keybinding Changes
- Added F7/F8 for brightness (using brightnessctl)
- Added SUPER+L for lock
- Removed ALT+F4 power menu (use panel instead)
- Added screenshot bindings
- Added clipboard history (SUPER+X)
- Added blue light filter toggle (SUPER+N)

### Removed/Deleted
- All custom bash scripts (user hates them)
- Auto-suspend timeout
- Wofi references and package (uses hyprlauncher)
- Mako notification daemon (was removed earlier)
- HyprPanel (broken systray, replaced with Waybar)
- Taskbar from panel
- Date from clock
- Default Hyprland autogenerated comments/boilerplate
- Hyprland anime mascot wallpaper/logo
- Epic-mouse-v1 example device config
- NVIDIA power env vars (handled by CachyOS + asusctl)

### WiFi / Bluetooth / VPN
- nm-applet (--indicator) and blueman-applet run as tray applets in Waybar systray
- Autostart via hyprland.conf exec-once
- User overrides in ~/.config/autostart/ for nm-applet.desktop and blueman.desktop
- NetworkManager is the backend, currently on WiFi "moto" (wlan0)
- **IIIT VPN** configured in NetworkManager (OpenVPN, vpn.iiit.ac.in:1194 UDP)
  - Username: adithya.jillellamudi@students.iiit.ac.in
  - Password stored in NM connection secrets
  - CA cert: ~/.cert/iiit-vpn-ca.crt
  - Source .ovpn files: ~/iiit_vpn_working.ovpn, ~/iiit_vpn_complete.ovpn
  - Connect via nm-applet tray or: `nmcli connection up "IIIT VPN"`
- Notifications: mako (reinstalled, pitch black theme in ~/.config/mako/config)

### Environment Variables (set in hyprland.conf)
- Toolkit backends: GDK_BACKEND, QT_QPA_PLATFORM, SDL_VIDEODRIVER, CLUTTER_BACKEND
- XDG session: XDG_CURRENT_DESKTOP, XDG_SESSION_TYPE, XDG_SESSION_DESKTOP
- QT theming: QT_AUTO_SCREEN_SCALE_FACTOR, QT_QPA_PLATFORMTHEME, QT_WAYLAND_DISABLE_WINDOWDECORATION
- GTK: GTK_THEME=Adwaita:dark
- NVIDIA: LIBVA_DRIVER_NAME, __GLX_VENDOR_LIBRARY_NAME, NVD_BACKEND (REMOVED - handled by CachyOS)
- Cursor: XCURSOR_SIZE=24, HYPRCURSOR_SIZE=24, XCURSOR_THEME=Adwaita
- Electron: ELECTRON_OZONE_PLATFORM_HINT=auto

### GTK Dark Mode
- Set via gsettings: color-scheme=prefer-dark, gtk-theme=Adwaita-dark
- Also set via env: GTK_THEME=Adwaita:dark
- Portal env propagated via dbus-update-activation-environment on startup

### Refresh Rate Switching
- C binary at ~/.local/bin/refresh-switch (15KB, ~800KB cgroup memory)
- Source at ~/refresh-switch-c/refresh-switch.c (single file, sd-bus)
- Rust reference version at ~/refresh-switch/ (kept but not in use)
- Systemd service at ~/.config/systemd/user/refresh-switch.service
- Monitors D-Bus UPower signals for AC/battery state changes (zero polling)
- AC: 240Hz
- Battery: 60Hz
- ONLY switches refresh rate, no power profile or battery limit changes
- Build: `cd ~/refresh-switch-c && make && make install`

## Troubleshooting

### Keys Not Working
- Reload config: `hyprctl reload`
- Check bindings: `hyprctl binds | grep key-name`
- Test command manually first
- Ensure package is installed

### Services Not Starting
- Check if running: `pgrep service-name`
- Kill and restart: `pkill service && service &`
- Check logs: `journalctl -u service-name -f`

### Brightness Not Working
- Ensure brightnessctl installed
- Check device exists: `ls /sys/class/backlight/`
- Use intel_backlight device
- User is in 'video' group

## Notes for Future Sessions

- User is technical and knows what they want
- Don't be overly cautious - just do it
- Config file changes > scripts
- Test with actual commands before adding to config
- Keep everything minimal and clean
- Pitch black theme everywhere
- No unnecessary bloat
