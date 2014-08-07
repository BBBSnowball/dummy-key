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

If you already have another `id_rsa`, use a different name and create an appropriate SSH config file. You can do that like this:

```sh
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

Set `GIT_SSH` when cloning repositories from Github, e.g. `GIT_SSH="path/to/dummy-key/dummy-ssh" git submodule update --init your-github-submodule`.

You should deploy a copy of dummy-key in your repository, so your scripts know where to find it. Of course, this submodule cannot use an SSH URL.

Example:
```sh
mkdir deps
git submodule add https://github.com/BBBSnowball/dummy-key deps/dummy-key
git submodule add git@github.com:some-awesome-software.git deps/some-awesome-software
cat >fetch.sh <<EOF
git submodule update --init deps/dummy-key
GIT_SSH="deps/dummy-key/dummy-ssh" git submodule update --init deps/some-awesome-software
EOF
```
