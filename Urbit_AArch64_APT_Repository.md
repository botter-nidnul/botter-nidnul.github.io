---
title: Urbit AArch64 APT Repository
description: Steps to easily and automatically install Urbit as a debian package 
---

↰ [Return to Index](index.md)

# Urbit AArch64 APT Repository

If you're running a debian derivative, you can install Urbit as a debian package:

#### Import the repository signing key

`curl https://s3.us-east-2.amazonaws.com/urbit-on-arm/urbit-on-arm_public.gpg | sudo apt-key add -`

#### Add the repository to your apt sources

In case this linewraps on your screen, this is supposed to all be on one line:

```
echo 'deb http://urbit-on-arm.s3-website.us-east-2.amazonaws.com buster custom' | sudo tee /etc/apt/sources.list.d/urbit-on-arm.list
```

#### Update the package list

`sudo apt update`

#### Install Urbit

`sudo apt install urbit`

#### If you get an error on a 32-bit distro

If you see the message `repository 'http://urbit-on-arm.s3-website.us-east-2.amazonaws.com buster InRelease' doesn't support architecture 'armhf'` try enabling multiarch for arm64.

`sudo dpkg --add-architecture arm64`

run `sudo apt update` again

and then `sudo apt-get install urbit:arm64`

↰ [Return to Index](index.md)
