# Qtile Configuration - Installation Guide

## Required Dependencies

### Core Requirements
```bash
# Qtile and Python
sudo pacman -S qtile python-psutil python-dbus-next

# Terminal
sudo pacman -S kitty

# Font
sudo pacman -S ttf-consolas  # Consolas font
# OR if not available in main repos:
yay -S ttf-consolas

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
   font_family Consolas
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
- `Super + c` - Close window
- `Super + f` - Toggle fullscreen
- `Super + t` - Toggle floating
- `Super + Tab` - Cycle layouts

**Workspaces:**
- `Super + www/term/code/music/etc` - Switch to workspace
- `Super + Shift + www/term/code/music/etc` - Move window to workspace

**Applications:**
- `Super + Return` - Open Kitty terminal
- `Super + Space` - Open Rofi (app launcher)
- `Super + r` - Open Rofi (app launcher)
- `Super + p` - Open Rofi (run commands)

**System:**
- `Super + Control + r` - Reload config
- `Super + Control + q` - Quit qtile
- `Print` - Screenshot (flameshot)

**Media Keys:**
- `F11` - Volume up
- `F10` - Volume down
- Volume mute (media key)
- Brightness up/down (laptops)

### Layout Features

- **Border width:** 2px
- **Window gaps:** 8px all around
- **Borders always visible:** Even single windows have borders
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

**Bar height:** 36px (not floating, attached to screen edge)

**Left:**
- 🐧 Penguin icon (clickable - opens rofi)
- Workspace indicators: www, term, code, music, etc
- Violet highlight block when workspace is active

**Center:**
- 📆 Date icon
- Full date format: "12 February Wednesday"

**Right:**
- 💻 CPU usage percentage
- 🧠 RAM usage percentage
- 🔊 Volume percentage
- ⏱️ Time in 12-hour format: "01:10 PM"
- System tray (auto-shows when apps need it)

### Design Rationale

**Why these choices:**

1. **Catppuccin Mocha:** Popular, easy on the eyes, great contrast, widely supported
   - *Trade-off:* Slightly lower contrast than some themes, but better for extended use

2. **8px gaps:** Balance between visual appeal and screen real estate
   - *Alternative:* Reduce to 5px for more space, increase to 12px for aesthetics
   - *Trade-off:* Less gap = more usable space, but harder to distinguish windows

3. **2px borders always visible:** Ensures you always know window boundaries
   - *Trade-off:* Slight pixel loss, but massive improvement in visual clarity
   - *Logic:* Single window still needs borders to show it's a window, not fullscreen

4. **Consolas font:** Clean, readable monospace font that works universally
   - *Trade-off:* Less "fancy" than Nerd Fonts, but doesn't require special setup
   - *Efficiency:* System font = no extra downloads, instant rendering

5. **Named workspaces (www, term, code, music, etc):** Semantic organization
   - *Alternative:* Numbers (1-9) or icons
   - *Trade-off:* Typing full names vs. single digit, but clearer purpose
   - *Logic:* "www" is more memorable than "1" for browser workspace

6. **36px bar (not floating):** Maximum usability and readability
   - *Trade-off:* Uses more vertical space, but easier to read and click
   - *Logic:* Floating bars look cool but waste gaps; attached bars maximize space

7. **Emoji icons (💻🧠🔊⏱️📆🐧):** Universal, no font dependencies
   - *Alternative:* Nerd Font icons (require specific fonts)
   - *Trade-off:* Emojis may render differently across systems, but work everywhere
   - *Efficiency:* No font package needed, instant compatibility

8. **F11/F10 for volume:** Accessible without modifier keys
   - *Logic:* Media keys might not be available on all keyboards
   - *Trade-off:* Uses function keys, but more universally available

9. **Mod+Space for rofi:** Most ergonomic launcher combo
   - *Alternative:* Mod+r (also available as fallback)
   - *Logic:* Space is large thumb key = fastest access

10. **Mod+c to close window:** Follows vim/tmux conventions
    - *Alternative:* Mod+w is common in other WMs
    - *Trade-off:* Different from some WMs, but matches terminal workflows

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
# Emojis should work by default on most systems
# If they don't render, install:
sudo pacman -S noto-fonts-emoji
```

**Workspaces not accessible by typing:**
```bash
# Named workspaces require typing the full name
# Example: Super+w+w+w for "www" workspace
# This is a qtile limitation with multi-char group names
# Alternative: modify config to use single letters (w, t, c, m, e)
```

**Consolas font not found:**
```bash
# Try installing from AUR
yay -S ttf-consolas
# Or use alternative monospace font like:
# - ttf-dejavu
# - ttf-liberation
# Edit config.py and change font="Consolas" to your chosen font
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
