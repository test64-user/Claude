# Qtile Configuration - Installation Guide

## Required Dependencies

### Core Requirements
```bash
# Qtile and Python
sudo pacman -S qtile python-psutil python-dbus-next

# Terminal
sudo pacman -S kitty

# Font
yay -S ttf-meslo-nerd-font-powerlevel10k
# OR
sudo pacman -S ttf-meslo-nerd

# Application Launcher
sudo pacman -S rofi

# System utilities
sudo pacman -S pulseaudio pamixer  # For volume control
sudo pacman -S brightnessctl  # For brightness control (laptops)

# Screenshot tool
sudo pacman -S flameshot

# X11 utilities
sudo pacman -S xorg-xsetroot xorg-xrdb feh

# Cursor theme (Adwaita - usually comes with GNOME packages)
sudo pacman -S adwaita-icon-theme
```

### Optional but Recommended
```bash
# Compositor for transparency and effects
sudo pacman -S picom

# Wallpaper setter
sudo pacman -S nitrogen

# Network manager applet (for systray)
sudo pacman -S network-manager-applet

# Volume control GUI
sudo pacman -S pavucontrol

# File manager
sudo pacman -S thunar  # or pcmanfm, nautilus, etc.
```

## Installation Steps

1. **Install all dependencies** (see above)

2. **Create qtile config directory:**
   ```bash
   mkdir -p ~/.config/qtile
   ```

3. **Copy the config file:**
   ```bash
   cp config.py ~/.config/qtile/config.py
   ```

4. **Set up .Xresources** (if you don't have one):
   ```bash
   touch ~/.Xresources
   ```
   
   Example `.Xresources` content:
   ```
   ! Cursor theme
   Xcursor.theme: Adwaita
   Xcursor.size: 16
   
   ! Terminal colors (Catppuccin Mocha for consistency)
   *.foreground: #CDD6F4
   *.background: #1E1E2E
   *.color0: #45475A
   *.color8: #585B70
   *.color1: #F38BA8
   *.color9: #F38BA8
   *.color2: #A6E3A1
   *.color10: #A6E3A1
   *.color3: #F9E2AF
   *.color11: #F9E2AF
   *.color4: #89B4FA
   *.color12: #89B4FA
   *.color5: #F5C2E7
   *.color13: #F5C2E7
   *.color6: #94E2D5
   *.color14: #94E2D5
   *.color7: #BAC2DE
   *.color15: #A6ADC8
   ```

5. **Configure Kitty terminal** with Meslo font and Catppuccin theme:
   ```bash
   mkdir -p ~/.config/kitty
   nano ~/.config/kitty/kitty.conf
   ```
   
   Add to `kitty.conf`:
   ```
   # Font
   font_family MesloLGS Nerd Font
   bold_font auto
   italic_font auto
   bold_italic_font auto
   font_size 11.0
   
   # Catppuccin Mocha Theme
   foreground #CDD6F4
   background #1E1E2E
   selection_foreground #1E1E2E
   selection_background #F5E0DC
   
   cursor #F5E0DC
   cursor_text_color #1E1E2E
   
   url_color #89B4FA
   
   # Black
   color0 #45475A
   color8 #585B70
   
   # Red
   color1 #F38BA8
   color9 #F38BA8
   
   # Green
   color2 #A6E3A1
   color10 #A6E3A1
   
   # Yellow
   color3 #F9E2AF
   color11 #F9E2AF
   
   # Blue
   color4 #89B4FA
   color12 #89B4FA
   
   # Magenta
   color5 #F5C2E7
   color13 #F5C2E7
   
   # Cyan
   color6 #94E2D5
   color14 #94E2D5
   
   # White
   color7 #BAC2DE
   color15 #A6ADC8
   
   # Tab bar
   tab_bar_style powerline
   tab_powerline_style slanted
   ```

6. **Test the configuration:**
   ```bash
   qtile cmd-obj -o cmd -f validate_config
   ```

7. **Reload qtile** (if already running):
   ```bash
   # Press: Super + Control + R
   ```
   
   Or restart your X session to apply cursor changes.

## Configuration Details

### Keybindings

**Window Management:**
- `Super + h/j/k/l` - Move focus (vim-style)
- `Super + Shift + h/j/k/l` - Move window
- `Super + Control + h/j/k/l` - Resize window
- `Super + n` - Reset window sizes
- `Super + w` - Close window
- `Super + f` - Toggle fullscreen
- `Super + t` - Toggle floating
- `Super + Tab` - Cycle layouts

**Workspaces:**
- `Super + [1-9]` - Switch to workspace
- `Super + Shift + [1-9]` - Move window to workspace

**Applications:**
- `Super + Return` - Open Kitty terminal
- `Super + r` - Open Rofi (app launcher)
- `Super + p` - Open Rofi (run commands)

**System:**
- `Super + Control + r` - Reload config
- `Super + Control + q` - Quit qtile
- `Print` - Screenshot (flameshot)

**Media Keys:**
- Volume up/down/mute
- Brightness up/down (laptops)

### Layout Features

- **Border width:** 2px
- **Window gaps:** 10px all around
- **Focus color:** Catppuccin Mauve (violet)
- **Normal color:** Catppuccin Surface0 (dark gray)

Available layouts:
1. Columns (default)
2. Max (monocle)
3. MonadTall (master-stack)
4. MonadWide (wide master-stack)
5. BSP (binary space partition)
6. Floating

### Bar Features

**Left:**
- Custom Arch icon (clickable - opens rofi)
- Workspace indicators with violet highlight when active

**Center:**
- Full date format: "12 February Wednesday"

**Right:**
- CPU usage with icon
- RAM usage with icon
- Volume with icon
- Time in 12-hour format: "01:10 PM"
- System tray (auto-shows when apps need it)

### Design Rationale

**Why these choices:**

1. **Catppuccin Mocha:** Popular, easy on the eyes, great contrast, widely supported
   - *Trade-off:* Slightly lower contrast than some themes, but better for extended use

2. **10px gaps:** Balanced between visual appeal and screen real estate
   - *Alternative:* Reduce to 5px for more space, increase to 15px for aesthetics
   - *Trade-off:* More gaps = less usable space but clearer window separation

3. **2px borders:** Visible without being intrusive
   - *Trade-off:* Could go borderless with good compositor, but harder to see focus

4. **Vim-style navigation (hjkl):** Efficient for keyboard users
   - *Alternative:* Arrow keys work but less ergonomic
   - *Trade-off:* Learning curve if new to vim-style

5. **Widget order:** Most dynamic info on right (typical pattern)
   - *Logic:* Eyes naturally scan left-to-right, so static/context stays left

6. **Multiple layouts:** Flexibility for different workflows
   - *Trade-off:* More to learn, but can stick to 1-2 favorites

7. **Startup hook for .Xresources:** Ensures consistent theming
   - *Efficiency:* Slight startup delay, but one-time per session

### Optimizations

**Current config is optimized for:**
- Low resource usage (qtile is lightweight)
- Fast window switching
- Minimal visual clutter

**Possible improvements:**
1. Add picom for smooth animations (trade-off: ~2-5% CPU usage)
2. Use compositor with blur (trade-off: more GPU usage, looks amazing)
3. Add more widgets (trade-off: more info vs. cleaner bar)
4. Implement scratchpad for dropdown terminal (efficiency boost)

## Troubleshooting

**Icons not showing:**
```bash
# Make sure nerd font is installed and selected
fc-list | grep -i meslo
```

**Cursor not changing:**
```bash
# Set in ~/.Xresources and reload
xrdb -merge ~/.Xresources
# Then restart X session
```

**Volume widget not working:**
```bash
# Check if pulseaudio/pipewire is running
pactl info
```

**Systray items not appearing:**
- Some apps need to be launched with `--hidden` flag
- Check if app supports system tray

## Additional Customization

**Change theme colors:**
Edit the `catppuccin` dictionary in config.py

**Adjust gaps:**
Change `margin` value in `layout_theme`

**Modify bar height:**
Change the value in `bar.Bar(..., 30, ...)` (currently 30px)

**Add more startup apps:**
Edit the `autostart()` function

## Resources

- [Qtile Documentation](http://docs.qtile.org/)
- [Catppuccin Theme](https://github.com/catppuccin/catppuccin)
- [Nerd Fonts](https://www.nerdfonts.com/)
- [Arch Wiki - Qtile](https://wiki.archlinux.org/title/Qtile)
