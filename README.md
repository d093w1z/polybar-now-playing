# polybar-now-playing
Script for polybar to display and control media(not only Spotify) using DBus

Python script to display and control current playing media. Includes a way to switch between players.
Scrolling text used for metadata(title and artist) and playback button based on [spotify-polybar](https://github.com/PrayagS/polybar-spotify) and [zscroll](https://github.com/noctuid/zscroll).

#### Demo:
![demo](demo.gif)

![screenshot](screenshot.png)

### Dependencies

- [python3](https://www.python.org/downloads/): Required to run the script
- [playerctl](https://github.com/altdesktop/playerctl): Required to control players
- [dbus-python](https://pypi.org/project/dbus-python/): python module required to interact with [DBus](https://www.freedesktop.org/wiki/Software/dbus/) message bus system

### Setup
- This script requires a monospace font to work as expected, so adding a monospace font to your polybar config is adviced. After adding the font, update the index in `polybar-now-playing` file where indicated.
Font indices are 1-based so be careful, refer [polybar:Fonts](https://github.com/polybar/polybar/wiki/Fonts#fonts).

```python3
# Config options

# (int) : Length of media info string. If length of string exceedes this value,
# the text will scroll. Default value is 20.
message_display_len = 20

# (int) : Font index of polybar. this value should be 1 more than the font
# value specified in polybar config.
font_index = <font index defined in polybar config> + 1


# (float) : Update speed of the text in seconds. Default value 0.3.
update_delay = 0.3

# (list) : list of chars containing previous, play, pause, next glyphs
# for media controls in respective order
control_chars = ['','','','']

# (dict) : dict of char icons to display as prefix.
# If player name is available as key, then use the corressponding icon,
# else default.
# example:
display_player_prefix = {
    "spotify":  '',
    "firefox":  '',
    "default":  ''
}
```

- After setting the options, add the following to your polybar config.

```ini
[module/now-playing]
type = custom/script
tail = true
;format-prefix = ""
format = <label>
exec = <path/to/script>
click-right = "kill -USR1 $(pgrep --oldest --parent %pid%)"
```
