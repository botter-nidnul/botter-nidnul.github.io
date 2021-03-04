---
title: Steps to Urbit on Raspberry Pi
description: Guide for running (and optionally building) Urbit on the Raspberry Pi
---

↰ [Return to Index](index.md)

# Steps to Urbit on Raspberry Pi

You need a Raspberry Pi capable of running in AArch64 (aka 64-bit) mode, which means a RPi 3 or 4 (maybe a later model RPi 2 with the upgraded BCM2837 chip). The CPUs of earlier models will struggle with providing a smooth interactive experience, and the RPi3 and RPi2 are probably better suited to [moon tasks](https://urbit.org/docs/glossary/moon/) that don't need much responsiveness.

Be aware that running Urbit on a microSD card may contribute to a slower Urbit experience, depending on the speed of your card and the speed of the reader in your Raspberry Pi, and if you're running anything else on the device that will compete with Urbit for disk access. On models earlier than the Raspberry Pi 4 there may be benefit to [overclocking the reader interface](https://www.jeffgeerling.com/blog/2016/how-overclock-microsd-card-reader-on-raspberry-pi-3) to increase the speed the microSD card can be written to.

It's better to avoid the microSD card and just run your Pi from a USB3 attached SSD (get an adapter that supports [UASP](https://www.jeffgeerling.com/blog/2020/uasp-makes-raspberry-pi-4-disk-io-50-faster)).

It's best to avoid buying a Raspberry Pi entirely, and to instead [purchase an alternative single-board computer](Buying_Guide.md) with sane storage options built into the board.

### OS Version

This guide assumes you're running the latest ([Buster](https://www.raspberrypi.org/blog/buster-the-new-version-of-raspbian/)) 32-bit (armv7l) version of the default Raspberry Pi distro "Raspberry Pi OS" (previously called Raspbian) and that you've run `sudo apt update` and `sudo apt full-upgrade` recently.

### Step One: Kernel

You need to add `arm_64bit=1` to `/boot/config.txt`.

You can do this by running `echo 'arm_64bit=1' | sudo tee -a /boot/config.txt`

*Make sure to not leave out the `-a` after `tee` or your /boot/config.txt file will consist of nothing but arm_64bit=1*

Now reboot and your Pi will be running a 64-bit kernel.

### Step Two: Import the repository signing key

```
curl https://s3.us-east-2.amazonaws.com/urbit-on-arm/urbit-on-arm_public.gpg | sudo apt-key add -
```

### Step Three: Add the repository to your apt sources

```
echo 'deb http://urbit-on-arm.s3-website.us-east-2.amazonaws.com buster custom' | sudo tee /etc/apt/sources.list.d/urbit-on-arm.list
```

### Step Four: Enable multiarch for arm64

`sudo dpkg --add-architecture arm64`

### Step Five: Update the package list

`sudo apt update`

Messages like the below are expected and harmless:

```
N: Skipping acquire of configured file 'custom/binary-armhf/Packages' as repository 'http://urbit-on-arm.s3-website.us-east-2.amazonaws.com buster InRelease' doesn't support architecture 'armhf'
N: Skipping acquire of configured file 'main/binary-arm64/Packages' as repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' doesn't support architecture 'arm64'
N: Skipping acquire of configured file 'contrib/binary-arm64/Packages' as repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' doesn't support architecture 'arm64'
N: Skipping acquire of configured file 'non-free/binary-arm64/Packages' as repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' doesn't support architecture 'arm64'
N: Skipping acquire of configured file 'rpi/binary-arm64/Packages' as repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' doesn't support architecture 'arm64'

```

### Step Five: Actually install Urbit

`sudo apt install urbit`

### Step Six: Boot Your Planet

Run urbit with `urbit some-planet` (note there's no `./` in front of the urbit command like when you use the usual binaries from `linux64.tgz`).

So booting a comet would be `urbit -c mycomet` and running that comet would be `urbit mycomet`, and booting a planet would be `urbit -w sampel-palnet -k ./my-planet.key`.

So you can follow the [install guide from urbit.org](https://urbit.org/using/install/) but don't put what it tells you to in front of the `urbit` part of the command.

There's also no need to run `sudo setcap 'cap_net_bind_service=+ep'` to allow urbit to bind to port 80, it's already been done for you as part of the package install process.

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
