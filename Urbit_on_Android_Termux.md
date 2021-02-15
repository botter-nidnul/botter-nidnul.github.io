---
title: Urbit on Android (Termux)
description: A guide to getting Urbit running on your Android device 
---

↰ [Return to Index](index.md)

### A guide to getting Urbit running on your Android device.

Running Urbit on Android requires Termux, and using PRoot to get around Android security "features".

Your Android device will need to have at least a linux kernel version of 3.17 because of [libent](https://github.com/urbit/libent).

These Termux Urbit binaries have been modified to run on Android by altering the [LMDB build flags](https://github.com/botter-nidnul/urbit/commit/f5fd8cec3a71fec42e9584e943f2e00dde83d646).

### Step One: Install Termux

From the [Play Store](https://play.google.com/store/apps/details?id=com.termux) or
[F-Droid](https://f-droid.org/repository/browse/?fdid=com.termux)

### Step Two: Disable Powersaving

Start up Termux, then access the notification panel from the top of your screen, and click Termux's notification - you'll want to acquire wakelock to keep your Urbit running.

You'll also want to make sure battery optimization (or whatever your particular version of Android calls it) has been turned off for Termux. This is supposed to happen automatically the first time you tell Termux to acquire wakelock, but it didn't seem to happen for me. This option will be deeply buried somewhere in the settings app.

Your particular ROM may have an aggressive process killer that will murder Termux if it runs too intensively for too long. I've personally suffered from OnePlus's BgDetect, which I prevent from doing its dirty work by opening the recent apps switcher, clicking on the three dots in the upper right hand corner of the Termux screenshot and clicking "🔒Lock".

### Step Three: Install Pkgs

Install the necessary packages:

`pkg install resolv-conf proot`

### Step Four: Get Binaries

```
curl -OL https://github.com/botter-nidnul/urbit/releases/download/urbit-v1.2-android/urbit-v1.2-4d48b.tar.gz
tar xzf urbit-v1.2-4d48b.tar.gz
```

### Step Five: Run Urbit

You need to run `termux-chroot` to switch into a PRoot'ed environment, then you can start Urbit just like you would in normal linux:

```
termux-chroot
./urbit-v1.2-aarch64-linux/urbit sampel-palnet
```

### Step Six: Feedback

It'd be helpful if you give feedback on where this does or doesn't work in the group on Urbit `~dasfeb/smol-computers`

↰ [Return to Index](index.md)
