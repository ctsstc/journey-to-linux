
# Github

## Keys

<https://github.com/settings/keys>

**Note**: Make sure to be on the Linux instructions 😉

### Add SSH Key

https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-linux

### Add GPG Key

https://help.github.com/en/articles/managing-commit-signature-verification

#### SAVE YOURSELF PLEASE!

Do not waste the time and the deep rabit hole of issues that manually installing `gpg2` will consume of you.

Just brew install it. 

It will take a long time, but soooo much better having it automated rather than doing it all by hand 😢

```bash
brew install gpg2
```

#### Notes

You can use something besides `gpg` to sign your commits. According to their link you can use `X.509` instead.

- https://help.github.com/en/articles/telling-git-about-your-signing-key
- https://github.com/github/smimesign

> Because I only found this out after I was near the end of the Github setup instructions where they finally mention it at the end. I was even searching without luck [knowing something did exist from previous setups]. I wasted far too much time installing the latest version of `gpg` by hand and fixing things along the way.
