# Steps to Urbit on Raspberry Pi

You need a Raspberry Pi capable of running in AArch64 (aka 64-bit) mode, which means a RPi 3 or 4 (maybe a later model RPi 2 with the upgraded BCM2837 chip).

This guide assumes you're running the latest ([Buster](https://www.raspberrypi.org/blog/buster-the-new-version-of-raspbian/)) version of the default Raspberry Pi distro, Raspbian, and that you've run `sudo apt update` and `sudo apt upgrade` recently.

### Step One: Kernel

You need to add `arm_64bit=1` to `/boot/config.txt`.

You can do this by running `echo 'arm_64bit=1' | sudo tee -a /boot/config.txt`

*Make sure to not leave out the `-a` after `tee` or your /boot/config.txt file will consist of nothing but arm_64bit=1*

Now reboot and your Pi will be running a 64-bit kernel.

### Alternate Step Two: Download Static Binaries

It's now possible to download already compiled static binaries for AArch64. See [this post](AArch64_Urbit_Static_Binaries.md) for further details. If you take this route, the following steps are unnecessary.

### Step Two: Nix

`sudo mkdir /nix && sudo chown pi.pi /nix`

`curl https://nixos.org/nix/install | sh`

Then restart your shell session or run `. /home/pi/.nix-profile/etc/profile.d/nix.sh` so your environment variables are set for nix.

### Step Three: Git

`sudo apt-get install git-lfs`

`git clone https://github.com/urbit/urbit --branch urbit-v0.10.4`

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

You may get occasional [memory mapping errors on boot](https://github.com/urbit/urbit/issues/2067). These errors are intermittent, just try running urbit again.

If your Pi doesn't have enough ram to run urbit, [create a swap file](https://urbit.org/using/install/#about-swap-space).

### The Chat

Join the chat ~/~botter-nidnul/extreme-urbiting if you have questions or issues.
