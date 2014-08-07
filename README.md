*Before you ask: I do realize that this repository contains a private key.*

Dummy access key for Github / Gitlab
====================================

You can use this key for any machine that needs access to public Github repositories via SSH URLs,
but doesn't have any other credentials for Github.

This means that you can use SSH URLs for git submodules and still make it work anywhere.


How to use?
===========

For a machine
-------------

Copy `id_rsa` and `id_rsa.pub` to `~/.ssh`. Do *not* copy `config`. That's it.

If you already have another `id_rsa`, use a different name and create an appropriate SSH config file:

```
cp id_rsa     ~/.ssh/id_rsa_github
cp id_rsa.pub ~/.ssh/id_rsa_github.pub
cat >>~/.ssh/config <<EOF
Host github.com
    PubkeyAuthentication yes
    IdentityFile ~/.ssh/id_rsa_github
EOF
```

For a repository
----------------

Set `GIT_SSH` when cloning repositories from Github, e.g. `GIT_SSH="path/to/dummy-key/dummy-ssh" git fetch --init your-github-submodule`.
