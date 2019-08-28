# ~/.bashrc

## Keychain

Add ssh upon login.

Install `keychain`.

```shell
sudo apt-get install keychain
```

Add to `~/.bashrc`:

```shell
eval $(keychain --eval id_rsa)
```

If you want to silence it completely

```shell
eval $(keychain --eval id_rsa) >/dev/null 2>&1
```

> If you would like to redirect the output to logs:
>
> https://stackoverflow.com/questions/2292847/how-to-silence-output-in-a-bash-script
