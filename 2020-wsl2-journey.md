
## Pre-work & Install WSL2
- https://docs.microsoft.com/en-us/windows/wsl/compare-versions
- https://docs.microsoft.com/en-us/windows/wsl/wsl2-faq
- https://docs.microsoft.com/en-us/windows/wsl/install-win10
  - https://docs.microsoft.com/en-us/windows/wsl/install-win10#set-your-distribution-version-to-wsl-1-or-wsl-2

## New Environment
- `sudo apt update`
  - Needed to turn off the VPN so DNS would resolve /shrug
- `sudo apt upgrade`

## Install Fonts

You should do this before you install Powerlevel10k, so that the configuration displays the correct fonts.

Follow the instructions here. It will tell you how to install fonts for VSCode & Microsoft Terminal.
Download them, highlight, right click, install.

https://github.com/romkatv/powerlevel10k/blob/master/README.md#meslo-nerd-font-patched-for-powerlevel10k

### VS Code

Open _File_ → _Preferences_ → _Settings_, enter `terminal.integrated.fontFamily` in the search box and set the value to `MesloLGS NF`.

### Microsoft Terminal Settings

Add this to your corresponding profile after you have installed the fonts.

```json
"fontFace": "MesloLGS NF"
```

## Install ZSH & Oh My ZSH & Powerlevel 10k

```shell
# https://blog.nillsf.com/index.php/2020/02/17/setting-up-wsl2-windows-terminal-and-oh-my-zsh/
sudo apt install git zsh -y

# https://ohmyz.sh/#install
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Consider restarting/reopening a new shell
# https://github.com/romkatv/powerlevel10k
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
# Set ZSH_THEME="powerlevel10k/powerlevel10k" in ~/.zshrc.
# Restart/reopen a new shell
# You should be presented with the Powerlevel10k Conifguration Wizard
# You may want to get 
```

## Aliases

```shell
code ~/.zshrc

# Add these to `~/.zshrc`, should have some examples commented out near the bottom
alias projects="cd ~/projects"
```

> Protip: run `source ~/.zshrc` to reload the changes.

## ASDF Version Manager

- https://asdf-vm.com/
- https://github.com/asdf-vm/asdf
- https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/asdf

```shell
sudo apt install curl git
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.8.0

code ~/.zshrc
# Add `asdf` to plugins section ie: `plugins=(git asdf)`
```

### Install Node JS

```shell
asdf plugin-add nodejs git@github.com:asdf-vm/asdf-nodejs.git

# https://github.com/asdf-vm/asdf-nodejs/issues/119
bash ~/.asdf/plugins/nodejs/bin/import-release-team-keyring

# List available versions
asdf list-all nodejs
# Remember even major versions are LTS and odd are not
asdf install nodejs 14.15.1
# Set global so that npm/npx works
asdf global nodejs 14.15.1 
```

## Add SSH Key to Github

- https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
- https://github.com/settings/keys
  - IDK why that guide never links to this???
  - https://github.com/settings/ssh/new

```shell
# I tend to use no password if my system is already protected, and I use the same passwords anyways. Sloppy, but eh. 🤫
ssh-keygen -t ed25519 -C "YOUREMAIL@SOMEWHERE.COM"
ssh-add ~/.ssh/id_ed25519

# https://stackoverflow.com/questions/18695934/unable-to-copy-ssh-id-rsa-pub
# Be patient
clip < ~/.ssh/id_ed25519.pub
# or just cat it and copy it
cat ~/.ssh/id_ed25519.pub
```

## Add GPG Key to Github

- https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/managing-commit-signature-verification
  - https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-gpg-key#generating-a-gpg-key
- https://github.com/settings/keys
  - https://github.com/settings/gpg/new

### Generate a GPG Key

```shell
# Note: Size must be at least 4096
# No passphrase to avoid annoying VS Code integration with secure commits
gpg --full-generate-key

# Grab the hash from `sec`
# ie: sec   rsa4096/DEADBEEF1337 2020-11-28 [SC]
#  You would copy: DEADBEEF1337
gpg --list-secret-keys --keyid-format LONG

gpg --armor --export DEADBEEF1337
# or slow clipboard method
gpg --armor --export DEADBEEF1337 | clip.exe
```

## Use VSCode for Git Operations

- https://stackoverflow.com/questions/30024353/how-to-use-visual-studio-code-as-default-editor-for-git

```shell
git config --global core.editor "code --wait"
```

> Now you can use `git config --global -e`

## Configure Git

This will allow:
- To make commits with your name and email
- VSCode for Git Editor
- VSCode for Git Differencing & Merging
- Sign commits

**Note**: Change singing key with the hash from the GPG Generation step above.

- https://www.39digits.com/signed-git-commits-on-wsl2-using-visual-studio-code
- Didn't do the pinentry stuff since I did no password.

```gitconfig
[user]
	name = "Your Cool Name"
	email = "YOUREMAIL@SOMEWHERE.COM"
	signingkey = "DEADBEEF1337"
[commit]
	gpgsign = true
[tag]
	gpgsign = true
[core]
	editor = "code --wait"
[diff]
	tool = default-difftool
[difftool "default-difftool"]
	cmd = code --wait --diff $LOCAL $REMOTE
[merge]
	tool = vscode
[mergetool "vscode"]
	cmd = code --wait $MERGED
```

## Configure VSCode to Sign Commits

```json
"git.enableCommitSigning": true
```

## Fuzzy History

I NEED IT!

## Additional Dependencies

These will likely come in handy later, such as installing dependencies with npm.

```shell
sudo apt-get install build-essential

# https://askubuntu.com/questions/496549/error-you-must-put-some-source-uris-in-your-sources-list
# uncomment all deb-src lines
sudo nano /etc/apt/sources.list
sudo apt build-dep python3.9

asdf plugin-add python
asdf install python 3.9.0
```
