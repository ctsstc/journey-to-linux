
# Mouse Modifications

## Fix Mouse Wheel Freezing with VirtualBox

http://www.webupd8.org/2015/12/how-to-change-mouse-scroll-wheel-speed.html

### Install

```bash
sudo apt-get install imwheel
```

### Config

`~/.imwheelrc`

```bash
".*"
None,      Up,   Button4
None,      Down, Button5
Control_L, Up,   Control_L|Button4
Control_L, Down, Control_L|Button5
Shift_L,   Up,   Shift_L|Button4
Shift_L,   Down, Shift_L|Button5
```

### Startup

Add the following to your startup to help combat an issue with forward/back buttons.

Name: `Mouse Wheel Fixer Upper`

Command: `imwheel --kill --buttons "4 5"`

Comment: `http://www.webupd8.org/2015/12/how-to-change-mouse-scroll-wheel-speed.html`

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

## Mac Options

### Keyboard

In the scenario that you would like to remap the home or end buttons on a full keyboard to act like you would expect in Windows or most Linux systems to move the cursor to the start or end of a line. These may be potential options.

Remapping keys can likely be done natively with key binding configs, or utilizing something like Karabiner.

#### Karabiner

This is the powerhouse option for maximum configuration, supported by a community with custom mappings that you can choose to utilize.

- <https://karabiner-elements.pqrs.org/docs/manual/configuration/configure-simple-modifications/>

#### Simple Key Binding Configs

- <https://discussions.apple.com/thread/251108215?answerId=252138948022&sortBy=rank#252138948022>

```
mkdir -p $HOME/Library/KeyBindings
echo '{
/* Remap Home / End keys to be correct */
"\UF729" = "moveToBeginningOfLine:"; /* Home */
"\UF72B" = "moveToEndOfLine:"; /* End */
"$\UF729" = "moveToBeginningOfLineAndModifySelection:"; /* Shift + Home */
"$\UF72B" = "moveToEndOfLineAndModifySelection:"; /* Shift + End */
"^\UF729" = "moveToBeginningOfDocument:"; /* Ctrl + Home */
"^\UF72B" = "moveToEndOfDocument:"; /* Ctrl + End */
"$^\UF729" = "moveToBeginningOfDocumentAndModifySelection:"; /* Shift + Ctrl + Home */
"$^\UF72B" = "moveToEndOfDocumentAndModifySelection:"; /* Shift + Ctrl + End */
}' > $HOME/Library/KeyBindings/DefaultKeyBinding.dict
```  
