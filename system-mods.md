
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
