
# System Modifications

## Modify Terminal

### Up Arrow Auto Complete From History

This allows you to start typing something and then hit the up or down arrow to auto complete from your history off of what you already have typed rather than wiping out what you have and cylcing your history.

Put the following lines in your `~/.inputrc`:

```bash
## arrow up
"\e[A":history-search-backward
## arrow down
"\e[B":history-search-forward
```

> https://askubuntu.com/questions/59846/bash-history-search-partial-up-arrow

## Bash RC Mods

To reaload for the current terminal: `source ~/.bashrc`

### Quick Projects Folder Access

```bash
alias projects='cd ~/Projects'
```

### Clear Console + Buffer

This clears the console and the buffer so you cannot still scroll back up.

```bash
alias cls="echo -ne '\033c'"
```

### Fuzzy Search History

First you'll need to install fzf:

- <https://github.com/junegunn/fzf#installation>
- Additional Resource
  - <https://nickjanetakis.com/blog/fuzzy-search-your-bash-history-in-style-with-fzf>
  - <https://www.youtube.com/watch?v=DBGvWyQNYY0>

```bash
writecmd (){ perl -e 'ioctl STDOUT, 0x5412, $_ for split //, do{ chomp($_ = <>); $_ }' ; }

fh() {
  ([ -n "$ZSH_NAME" ] && fc -l 1 || history) | fzf +s --tac | sed -re 's/^\s*[0-9]+\s*//' | writecmd
}
```
