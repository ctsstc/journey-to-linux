
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
# You may or may not want to set the asdf global version, I did not
#  In hopes that it will load the latest /shrug
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



