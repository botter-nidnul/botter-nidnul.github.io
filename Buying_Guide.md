---
title: Buying Guide for Raspberry Pi Alternatives
description: What to look for in a Single-board Computer for running Urbit
---

↰ [Return to Index](index.md)

### What to look for in a Single-board Computer for running Urbit

Thinking about buying a Raspberry Pi just to run Urbit on it? I suggest you **don't** - you can **_do better than a Raspberry Pi!_** They're the most popular brand, and have the widest number of compatible accessories, but CPU and storage are both slower on the Raspberry Pi than on alternatives with the same or slightly higher price.

The Pi4 is powered by a BCM2711 with four Cortex-A72 cores running @ 1.5GHz. When looking for more performant chips search for something with at least two cores of Cortex-A72 design or better (eg Cortex-A73, Cortex-A75, etc) and with a higher frequency than 1.5GHz. Currently, the more powerful mainstream Pi alternatives are powered by the Rockchip RK3399, Amlogic S922X, or Amlogic A311D.

The Pi4 has very limited options for storage: either microsd cards that can be slow or prone to corruption, or through USB adapters that might have buggy chipsets or may not support [UASP](https://en.wikipedia.org/wiki/USB_Attached_SCSI). So be on the lookout for Pi alternatives with an eMMC module, an m.2 NVMe socket, or the ability to add on PCIe devices through a hat or riser.

A good place to start looking for RPi alternatives is [HackerBoards](https://hackerboards.com/).

At this point in time I'm a fan of the RK3399 powered [NanoPi M4V2](https://www.friendlyarm.com/index.php?route=product/product&path=69&product_id=268) which has a nice [passive heatsink option](https://www.friendlyarm.com/index.php?route=product/product&product_id=235), or a [metal case with fan and NVMe adapter](https://www.friendlyarm.com/index.php?route=product/product&path=89&product_id=267). For an option that looks less like a traditional Pi but has a more powerful CPU, consider an [ODroid N2+](https://www.hardkernel.com/shop/odroid-n2-with-4gbyte-ram-2/).

↰ [Return to Index](index.md)
