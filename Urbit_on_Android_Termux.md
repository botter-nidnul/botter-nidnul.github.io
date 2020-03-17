### A guide to (hopefully) getting Urbit running on your Android device.

**This guide is outdated:** you're almost certainly going to need a modified kernel or custom rom (or at least be rooted, and run the urbit binaries as root😬) if you're running Android 8 or above because of the seccomp "security feature".

There are two ways to do this: Inside of PRoot and outside of PRoot.

PRoot causes Urbit to run slowly; fast enough (on my device, YMMV) for a fake zod to have a responsive dojo (after an almost hour long first boot), but a comet or moon is almost unusable. The advantage to this approach is that you don't need a rooted device, and you can use the standard AArch64 Urbit binary.

Not using PRoot speeds up Urbit substantially, sufficiently to run a moon without the ames or behn spinner running almost constantly. This requires a [patched version of urbit](https://github.com/botter-nidnul/urbit/releases/tag/termux-v0.10.4) that knows where to find the tmp directory and resolv.conf file inside the normal Termux environment; it also requires your Android device to be rooted to circumvent the seccomp security feature which prevents static binaries from running.

The Android device will need to have at least a linux kernel version of 3.17 because of [libent](https://github.com/urbit/libent). There might be other problems with the kernel your device comes with. For example, I was only able to get this to work on my OnePlus 3T after upgrading to [this custom kernel](https://forum.xda-developers.com/oneplus-3/oneplus-3--3t-cross-device-development/r1b1-arter97-kernel-oneplus-3-3t-t4054539) which makes a number of alterations to the stock 3.18 kernel. I have no idea which of those changes was necessary to get this working. 

It'd be helpful if you give feedback on where it does or doesn't work, either in a comment here or in the chat ~botter-nidnul/extreme-urbiting

### Step One: Install Termux

From the [Play Store](https://play.google.com/store/apps/details?id=com.termux) or 
[F-Droid](https://f-droid.org/repository/browse/?fdid=com.termux)

### Step Two: Disable Powersaving

Start up Termux, then access the notification panel from the top of your screen, and click Termux's notification - you'll want to acquire wakelock to keep your Urbit running.

You'll also want to disable battery optimization (or whatever your particular version of Android calls it) for Termux which will be deeply buried somewhere in the settings app. (this is supposed to happen automatically the first time you tell termux to acquire wakelock, but it didn't seem to work for me)

### Step Three: Install Pkgs

Install some necessary packages:

`pkg install resolv-conf`

and if you're going to use PRoot:

`pkg install proot`

### Step Four: Get Binaries

Follow the `curl` and `tar` commands from the [AArch64 Static Binaries post](AArch64_Urbit_Static_Binaries.md).

If you're not going to use PRoot, modify the commands from the above link to use [this Termux release binary](https://github.com/botter-nidnul/urbit/releases/download/termux-v0.10.4/urbit-v0.10.4-termux-arm64.tgz)

If you're not using PRoot, you can then start Urbit just like you would in normal linux.

### Step Five: Run Urbit in PRoot

This command will mount the Termux prefix directory as the root of the filesystem, which will allow /tmp and /etc/resolv.conf to be found. The Termux home directory will be mounted inside this environment, sharing the home directory between the fake rootfs and the real one.

`proot -r $PREFIX -b $HOME:/home -w /home /home/ce095f1d381cdd12af4f09e5d7ab0c64c352ddf3-linux-arm64/urbit -F zod`
