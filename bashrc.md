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
