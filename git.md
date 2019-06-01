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
