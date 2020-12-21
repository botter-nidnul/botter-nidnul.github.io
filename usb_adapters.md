---
title: Public Service Announcement on USB attached SSDs
description: Getting a NVMe USB adapter to work properly requires doing your homework.
---

↰ [Return to Index](index.md)

## Public Service Announcement on USB attached SSDs

Since there’s more interest in external SSDs to run Bitcoin full nodes with Urbit on the Raspberry Pi, anyone planning to do this should know that there are some challenges with USB3 storage adapters.

This is why I suggest avoiding the Raspberry Pi in the [Buying Guide to Pi Alternatives](Buying_Guide.md) – get a NanoPi M4V2 with NVMe hat (still needs to boot from eMMC or microSD) or a Rock Pi 4C (can boot directly from NVMe, but at the cost of losing some compatibility with Raspberry Pi accessories that use SPI) and you don’t need to worry about most of this.

But if you want to use a Raspberry Pi, use caution with NVMe USB adapters - [the bugs haven’t all been worked out yet](https://forums.anandtech.com/threads/stable-nvme-usb-adapter.2572973). Be aware of the chipset used in the adapter, and also know that it might be necessary to upgrade the firmware of the controller to get it to behave well. It’s probably best to avoid adapters with the Micron JMS583 controller entirely - they tend to run hot. Instead look for adapters using the Realtek RTL9210 family or ASMedia ASM2362

Also be aware of the power draw of your NVMe drive - high performance SSDs like the Samsung 970 Evo can be very power hungry, and the USB connection of your Raspberry Pi can only supply 4.5W. Even when used in a NanoPi or Rock Pi you might want to avoid having anything extra drawing power when at full load (know what your USB power supply can provide).

Getting a NVMe USB adapter to work properly requires doing your homework. If you want fewer headaches, SATA is a more mature technology.

Regardless of your adapter being NVMe or SATA, **always remember to run `sudo systemctl enable fstrim.timer` on your Raspberry Pi** to enable TRIM to run on a weekly basis, as this is not something that is enabled by default on Raspberry Pi OS.

↰ [Return to Index](index.md)
