↰ [Return to Index](index.md)

### A guide to (hopefully) getting Urbit running on your Android device.

There are two ways to run Urbit on Android: Inside of PRoot and outside of PRoot.

The PRoot method will (with a little luck) allow you to run Urbit on a stock Android device, although at a slight speed penalty.

If you're running a custom kernel or custom ROM on your device it's likely [seccomp](https://en.wikipedia.org/wiki/Seccomp) has been disabled and you can run Urbit outside of PRoot. (To check the status of seccomp run `grep Seccomp /proc/self/status` in Termux. If seccomp is disabled this command will return either 0 or a blank line)

(It's also possible to get around seccomp on a rooted device running a stock kernel by launching Urbit as root. It's probably best not to do this, except *maybe* for a fake ~zod development ship. If you want to know how to run commands as root inside Termux you can look it up yourself.)

In my experience not using PRoot speeds up Urbit by about 7%, but with the poor single threaded performance of ARM chips you may find that actually makes a difference to your Urbit experience.

Both sets of these Termux Urbit binaries have been modified to run better on Android by altering the [LMDB build flags](https://github.com/botter-nidnul/urbit/commit/58ab2fbef177d8de9da10f8f8e407c6e3bc45295). The non-PRoot binaries have been further altered to know [where to find the tmp directory and resolv.conf file](https://github.com/botter-nidnul/urbit/commit/8ff6bc672d3975bb9ab1b1c2ec785d8273f81b75) inside the normal Termux environment.

Your Android device will need to have at least a linux kernel version of 3.17 because of [libent](https://github.com/urbit/libent). Android versions earlier than 8 (Oreo) do not have seccomp but may not have a kernel version high enough to run Urbit.

### Step One: Install Termux

From the [Play Store](https://play.google.com/store/apps/details?id=com.termux) or
[F-Droid](https://f-droid.org/repository/browse/?fdid=com.termux)

### Step Two: Disable Powersaving

Start up Termux, then access the notification panel from the top of your screen, and click Termux's notification - you'll want to acquire wakelock to keep your Urbit running.

You'll also want to make sure battery optimization (or whatever your particular version of Android calls it) has been turned off for Termux. This is supposed to happen automatically the first time you tell Termux to acquire wakelock, but it didn't seem to happen for me. This option will be deeply buried somewhere in the settings app.

Your particular ROM may have an aggressive process killer that will murder Termux if it runs too intensively for too long. I've personally suffered from OnePlus's BgDetect, which I prevent from doing its dirty work by opening the recent apps switcher, clicking on the three dots in the upper right hand corner of the Termux screenshot and clicking "🔒Lock".

### Step Three: Install Pkgs

Install some necessary packages:

`pkg install resolv-conf`

and if you're going to use PRoot:

`pkg install proot`

### Step Four: Get Binaries

If you're going to use PRoot:

```
curl -OL https://github.com/botter-nidnul/urbit/releases/download/termux-proot-v0.10.7/termux-proot-urbit-v0.10.7-linux-arm64.tgz
tar xzf termux-proot-urbit-v0.10.7-linux-arm64.tgz
```

If you're **not** going to use PRoot:

```
curl -OL https://github.com/botter-nidnul/urbit/releases/download/termux-v0.10.7/termux-urbit-v0.10.7-linux-arm64.tgz
tar xzf termux-urbit-v0.10.7-linux-arm64.tgz
```

### Step Five: Run Urbit

If you're **not** using PRoot, you can start Urbit just like you would in normal linux:

```
cd 01151dbaf73da0d8281f8bda27690adee10829bf-linux-arm64
./urbit
```

If you're using PRoot you need to run one extra command, `termux-chroot`, to switch into a PRoot'ed environment:

```
termux-chroot
cd 59a2aa0f71032028bb2fd9b4cdcac863655f1fab-linux-arm64
./urbit
```

### Step Six: Feedback

It'd be helpful if you give feedback on where this does or doesn't work, either in a comment here or in the chat ~/~botter-nidnul/extreme-urbiting

↰ [Return to Index](index.md)
