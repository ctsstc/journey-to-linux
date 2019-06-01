# Git

## Delimb

This adds a command so you can run `git delimb` and it will remove local branches that have been merged in and are no longer of use. Often this is more efficient than running `git fetch --prune`. It also protects `master` and `dev` branches.

### Open your global git config

```shell
git config -e --global
```

### Add `delimb` alias

```shell
[alias]
	delimb = !"f() { git branch --merged | egrep -v \"(^\\*|master|dev)\" || true | xargs git branch -d; }; f"
```

### Resources

- <https://stackoverflow.com/questions/6127328/how-can-i-delete-all-git-branches-which-have-been-merged>
- 