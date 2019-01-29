
# Developer Installations

## Configurations

### Git

#### Set Global Email

```bash
git config --global user.email "email@example.com"
```

#### Verify Global Email

```bash
git config --global user.email
```

#### VS Code as Git Editor

This will allow you to use VSCode for rebasing, commit messages, interactive adds, and diffing - if you edit the global git config as shown below.

```bash
## Set git editor to VSCode
git config --global core.editor "code --wait"
## View Global Git Config
git config --global -e
```

> <https://code.visualstudio.com/docs/editor/versioncontrol#_vs-code-as-git-editor>

#### VS Code as Git Diff Tool

```bash
## Open Global Git Config
git config --global -e
```

Add the following to the global git config.

```text
[diff]
    tool = default-difftool
[difftool "default-difftool"]
    cmd = code --wait --diff $LOCAL $REMOTE
```

> https://code.visualstudio.com/docs/editor/versioncontrol#_vs-code-as-git-diff-tool

## Installations

### Brew

Linux Brew: http://linuxbrew.sh/

### Node

- nvm
  - https://github.com/creationix/nvm#installation

### Ruby

- rvm
  - https://rvm.io/rvm/install

#### bundler

```shell
sudo apt install ruby-bundler
```

### VSCode

```shell
sudo apt install code
```
