# Git

## Delimb

This adds a command so you can run `git delimb` and it will remove local branches that have been merged in and are no longer of use. Often this is more efficient than running `git fetch --prune`. It also protects `master` and `dev` branches.

### Open your global git config

```shell
git config -e --global
```

### Add `delimb` alias

**Note**: This will check against the current branch you're on.

```shell
[alias]
	delimb = "!git branch --merged | grep  -v '\\*\\|master\\|develop' | xargs -n 1 git branch -d"
```

### Resources

- <https://stackoverflow.com/questions/6127328/how-can-i-delete-all-git-branches-which-have-been-merged>

## Other Config

### `.gitconfig`

This includes gpg signing, using VSCode as the difftool and mergetool, as well as some useful aliases like listing commits and the delimb alias mentioned above, but as a slight variation (maybe a better variation...)

```
[user]
	name = "Cody Swartz"
	email = "ctsstc@gmail.com"
	signingkey = XXXXXXXX
[commit]
	gpgsign = true
	template = /Users/coder/.gitmessage
[tag]
	gpgsign = true
[core]
	editor = "code --wait"
	excludesfile = /Users/coder/.gitignore_global
[diff]
	tool = default-difftool
[difftool "default-difftool"]
	cmd = code --wait --diff $LOCAL $REMOTE
[mergetool "vscode"]
	cmd = code --wait $MERGED
[gpg]
	program = /opt/homebrew/bin/gpg
	format = openpgp
[alias]
	l = log --graph --abbrev-commit --date=relative --pretty=format:\"%C(yellow)%h%Creset - %G? -%C(red)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset\" --topo-order
	la = !git l --all
	delimb = !git remote prune origin && git branch -vv | grep ': gone]' | awk '{print $1}' | xargs -r git branch -D
[pull]
	rebase = true
[init]
	defaultBranch = main
[push]
	autoSetupRemote = true
```

### `.gitmessage`

I don't often see this because I use VSCode's Source Control to make my commits. I believe you can still pull in the message there if you want, or utilize another commit tool/extension in VSCode. 

Tip: If you commit with an empty message it will pull up this template in VSCode's file pane.

```
# Short summary of change (the what) ( <= 50 chars )

# INTENTION of the change & REASON for change
# (Hard wrapped at 72 chars)

# APPROACH taken & WHY in relation to attempting to achieve INTENTION
# (Hard wrapped at 72 characters)

# Deployment or Rollout Considerations

# Automated Tests considerations - if **NOT** why?

# Associated Ticket Identifiers
# Ticket: 
# Sub Ticket: 

# Git Changelog header and entries if applicable
# [changelog]
# added: some addition you made that you want in your changelog
# changed: some change you made that you want in your changelog
# deprecated: some deprecation notice you want in your changelog
# removed: some removal you want in your changelog
# fixed: some fix you want in your changelog
# security: some security fix you want in your changelog


```
