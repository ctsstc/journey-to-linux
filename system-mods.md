
# System Modifications

## Modify Terminal

### Up Arrow Auto Complete From History

This allows you to start typing something and then hit the up or down arrow to auto complete from your history off of what you already have typed rather than wiping out what you have and cycling your history.

Put the following lines in your `~/.inputrc`:

```bash
## arrow up
"\e[A":history-search-backward
## arrow down
"\e[B":history-search-forward
```

> <https://askubuntu.com/questions/59846/bash-history-search-partial-up-arrow>

## Use ZSH

> https://blog.joaograssi.com/windows-subsystem-for-linux-with-oh-my-zsh-conemu/

```bash
sudo apt-get install zsh
```

### Oh My ZSH!

```bash
sudo apt-get install git
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

#### Configuration

Make sure it installed properly. You should find this in your `~/.bashrc` if it was installed correctly. If you do not see this add it.

```bash
if test -t 1; then
exec zsh
fi
```

#### Themes

Edit `~/.zshrc`

```bash
# Find and change this
ZSH_THEME="robbyrussell"

# To this
ZSH_THEME="agnoster"
```

#### Fonts

Install the powerline fonts for the agnoster theme.

**Note**: You will need to do this on Windows if you're running WSL.

```bash
git clone https://github.com/powerline/fonts.git
```

You may need to use Menlo for a monospaced font.

```bash
git clone https://github.com/abertsch/Menlo-for-Powerline.git
```

Another option: https://github.com/Homebrew/homebrew-cask-fonts

> **NOTE**: you may need to restart VSCode for the font to take hold.
> You may also have to set the `Terminal > Integrated: Font Family` to `Menlo for Powerline` for VSCode

## UI

### Appearance

- Dark Mode - Enable

### GNOME Tweaks

#### Window Titlebars

- Maximize - Enable
- Minimize - Enable
- Placement - Left

## Bash RC Mods

Modifications for `~/.bashrc`

To reload for the current terminal: `source ~/.bashrc`

### Quick Projects Folder Access

```bash
alias projects='cd ~/Projects'
```

### Clear Console + Buffer

This clears the console and the buffer so you cannot still scroll back up.

```bash
alias cls="echo -ne '\033c'"
```

> <https://superuser.com/questions/299903/clear-terminal-using-keyboard-shortcut>

### Fuzzy Search History

First you'll need to install fzf:

- <https://github.com/junegunn/fzf#installation>
- Additional Resource
  - <https://nickjanetakis.com/blog/fuzzy-search-your-bash-history-in-style-with-fzf>
  - <https://www.youtube.com/watch?v=DBGvWyQNYY0>

Then add this to your `.bashrc`

```bash
writecmd (){ perl -e 'ioctl STDOUT, 0x5412, $_ for split //, do{ chomp($_ = <>); $_ }' ; }

fh() {
  ([ -n "$ZSH_NAME" ] && fc -l 1 || history) | fzf +s --tac | sed -re 's/^\s*[0-9]+\s*//' | writecmd
}
```

After installing you may see something like:

```
==> fzf
To install useful keybindings and fuzzy completion:
  /home/linuxbrew/.linuxbrew/opt/fzf/install
```

Also consider running the installer mentioned above from the brew install.
This can enable:

- (CTRL-T, CTRL-R, ALT-C) to fuzzy search the current directory.
- Fuzzy searching completion ie: `cd /someDir/wh**`

```
cd /home/linuxbrew/.linuxbrew/opt/fzf
./install
```

### Increase History State Size

<https://askubuntu.com/questions/307541/how-to-change-history-size-for-ever>

```bash
HISTSIZE=5000
HISTFILESIZE=10000
```
