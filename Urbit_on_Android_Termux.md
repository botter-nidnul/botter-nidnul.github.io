---
title: Urbit on Android (Termux)
description: A guide to getting Urbit running on your Android device 
---

↰ [Return to Index](index.md)

## A guide to getting Urbit running on your Android device.

### Why?

Running Urbit on Android should be considered an experimental platform; a fun place for trying things out with a moon, rather than the best place to host your planet from.

I wouldn’t run it continuously for long stretches because Urbit writes more heavily to disk than it needs to right now, and a phone/tablet isn’t going to have enough spare disk capacity to absorb that wear. Also, Urbit doesn’t know how to put itself to sleep to conserve power, so it's going to affect your battery life.

What special things might you be able to do with Urbit on Android? There are some interesting addons for Termux (and they’re free if you install from F-Droid instead of the Google Play Store). So you could rig something up to have your Urbit send text messages, or collect information from your phone’s sensors. https://wiki.termux.com/wiki/Addons

There’s also Termux:Widget, which could make Urbit launch with the press of a button instead of having to type in the shell on your tiny keyboard.

### Technical details

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

### Step Three: Add APT Repo

Add my urbit-android repo to your Termux:

`curl -L https://botter-nidnul.github.io/urbit-android.deb/setup-urbit-repo.sh | sh`

### Step Four: Install Urbit

`pkg install urbit`

### Step Five: Run Urbit

You need to run `termux-chroot` to switch into a PRoot'ed environment, then you can start Urbit just like you would in normal linux:

```
termux-chroot
urbit sampel-palnet
```

### Step Five & 1/2: Help urbit-king find certificates

Termux doesn't have certificate information stored where `urbit-king` expects to find it, so if you want to use `urbit-king` first run `termux-chroot` and then `ln -s /etc/tls /etc/ssl`

### Step Six: Feedback

It'd be helpful if you give feedback on where this does or doesn't work in the group on Urbit `~dasfeb/smol-computers`

↰ [Return to Index](index.md)
