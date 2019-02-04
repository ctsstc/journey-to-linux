
# Mouse Modifications

## Remapping Mouse Forward and Back Buttons

In some cases some applications will not respond to mouse buttons 4 and 5 also known as 8 and 9. Most browsers handle this case but some applications are only expecting browser back or forward button events. This modification maps the mouse 8 and 9 respectively to the browser back and forward buttons.

I also tried out `XF86Back` and `XF86Forward` which worked fine in browsers, but VSCode did not pick up on them properly - it did catch them, but didn't fully recognize them to work. You can read more here... <https://github.com/Microsoft/vscode/issues/8641>

```bash
sudo apt install xbindkeys xdotool
```

Modify `~/.xbindkeysrc` with:

```bash
# Mouse Buttons
# Remap mouse buttons 8/9 to browser back/forward
"xdotool key ctrl+bracketleft"
  b:8
"xdotool key ctrl+bracketright"
  b:9
```

Reload `.xbindkeysrc` with:

```bash
xbindkeys --poll-rc
```

### Identifying Keys / Buttons

- `xev` is super helpful!
- <http://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap>

### Other Potential Options

#### xte

`~/.xbindkeysrc`

```bash
# Mouse Buttons
"xte key ctrl+bracketleft"
m:0x0 + b:8
"xte key ctrl+bracketright"
m:0x0 + b:9
```