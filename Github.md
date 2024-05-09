# Introduction
Used in conjunction with [[git]].
# Installation
# How To Use
## Connecting local repo to remote repo
SSH Key Integration Steps (taken from [Github's guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)):
  1. `ls -al ~/.ssh` to check for any existing keys
  2. `ssh-keygen -t ed25519 -C "<your-email-here>"` to create new ssh key (press Enter until clear)
  3. `cat ~/.ssh/id_ed25519.pub` to list out string to copy into Github for authentication