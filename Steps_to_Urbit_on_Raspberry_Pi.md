---
title: Steps to Urbit on Raspberry Pi
description: Guide for running (and optionally building) Urbit on the Raspberry Pi
---

↰ [Return to Index](index.md)

# Steps to Urbit on Raspberry Pi

You need a Raspberry Pi capable of running in AArch64 (aka 64-bit) mode, which means a RPi 3 or 4 (maybe a later model RPi 2 with the upgraded BCM2837 chip).

Be aware that running Urbit on a microSD card may, depending on the speed of your card and the speed of the reader in your Raspberry Pi, be a slow and frustrating experience. This is especially true on RPi models before the Raspberry Pi 4, which will need to have the [reader interface overclocked](https://www.jeffgeerling.com/blog/2016/how-overclock-microsd-card-reader-on-raspberry-pi-3) in order to run Urbit at an acceptable speed.

It's better to avoid the microSD card and just run your Pi from a USB attached SSD (get an adapter that supports [UASP](https://www.jeffgeerling.com/blog/2020/uasp-makes-raspberry-pi-4-disk-io-50-faster)).

It's best to avoid buying a Raspberry Pi entirely, and to instead [purchase an alternative single-board computer](Buying_Guide.md) with sane storage options built into the board.

### OS Version

This guide assumes you're running the latest ([Buster](https://www.raspberrypi.org/blog/buster-the-new-version-of-raspbian/)) 32-bit (armv7l) version of the default Raspberry Pi distro "Raspberry Pi OS" (previously called Raspbian) and that you've run `sudo apt update` and `sudo apt full-upgrade` recently.

### Step One: Kernel

You need to add `arm_64bit=1` to `/boot/config.txt`.

You can do this by running `echo 'arm_64bit=1' | sudo tee -a /boot/config.txt`

*Make sure to not leave out the `-a` after `tee` or your /boot/config.txt file will consist of nothing but arm_64bit=1*

Now reboot and your Pi will be running a 64-bit kernel.

## Alternate Step Two: Download Static Binaries

It's now possible to download already compiled static binaries for AArch64. See [this post](AArch64_Urbit_Static_Binaries.md) for further details. If you take this route, the following steps are unnecessary.

### Step Two: Nix

`sudo mkdir /nix && sudo chown pi.pi /nix`

`curl -L https://nixos.org/nix/install | sh`

Then restart your shell session or run `. /home/pi/.nix-profile/etc/profile.d/nix.sh` so your environment variables are set for nix.

### Step Three: Git

`sudo apt-get install git-lfs`

`git clone https://github.com/botter-nidnul/urbit --branch urbit-v1.0-aarch64`

`cd urbit`

### Step Four: Make

`make build && make install`

This step will take a while as nix needs to download and build urbit's dependencies.

### Step Five: Confirm Urbit Install

If step four completed successfully, `which urbit` should return `/home/pi/.nix-profile/bin/urbit`.

You no longer need the urbit directory git cloned, and I suggest you remove it to avoid confusion.

`cd`

`rm -rf urbit`

### Step Six: Boot Your Planet

Run urbit with `urbit some-planet` (note there's no `./` in front of the urbit command like when you use downloaded release binaries)

If your Pi doesn't have enough ram to run urbit, [create a swap file](https://raspberrypi.stackexchange.com/a/1605).

### Step Seven: Configure TRIM timer

Raspberry Pi OS doesn't set `fstrim` to run automatically, which can be a problem when combined with the way Urbit creates checkpoints; we need to discard the unused blocks from deleted checkpoint patches.

First, test if your storage device supports running fstrim.

run `sudo fstrim -v /` and it should produce results similar to:

`/: 13.1 GiB (14027571200 bytes) trimmed`

If it instead says:

`/: the discard operation is not supported`

then you may have an SD card that doesn't accept TRIM commands or issues with your USB SSD adapter, [which is a whole](https://www.glump.net/howto/desktop/enable-trim-on-an-external-ssd-on-linux) [complicated thing](https://www.jeffgeerling.com/blog/2020/enabling-trim-on-external-ssd-on-raspberry-pi) beyond the scope of this guide (and why I recommend avoiding the Raspberry Pi and buying a device with sane storage options built into the board.)

If `sudo fstrim -v /` produced successful results then change the timer to run more often and enable it:

`sudo sed -i 's/weekly/daily/' /lib/systemd/system/fstrim.timer`

`sudo systemctl enable fstrim.timer`

### The Group

Join the group `~dasfeb/smol-computers` if you have questions or issues.

↰ [Return to Index](index.md)
