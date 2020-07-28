↰ [Return to Index](index.md)

### What to look for in a Single-board Computer for running Urbit

Thinking about buying a Raspberry Pi 4 just to run Urbit on it? I suggest you **don't** - you can **_do better than a Raspberry Pi!_** They're the most popular brand, and have the widest number of compatible accessories, but CPU and storage are both slower on the Raspberry Pi than on alternatives with the same or slightly higher price.

(Note: It's possible to overclock the RPi4 and run everything except the /boot partition from a SSD over USB, but this guide is from the stock perspective, with out-of-box experience in mind.)

The Pi4 is powered by a BCM2711 with four Cortex-A72 cores running @ 1.5GHz. When looking for more performant chips search for something with at least two cores of Cortex-A72 design or better (eg Cortex-A73, Cortex-A75, etc) and with a higher frequency than 1.5GHz. Currently, the more powerful mainstream Pi alternatives are powered by the Rockchip RK3399, Amlogic S922X, or Amlogic A311D. (There are yet more powerful setups like the HiKey 960, but at that price they're competing with x86-64 SBCs, and I don't see the advantage)

Also be on the lookout for eMMC module or m.2 NVMe support. The RPi4 is primarily limited by its slow CPU, but the MicroSD card it must boot from can also reduce the speed of Urbit. Everything will be slightly snappier with better disk read/write performance. 

A good place to start looking for RPi alternatives is [HackerBoards](https://hackerboards.com/).

If I were to recommend a particular Pi alternative (which I'm not, because I haven't tried *_any_* of them) it would probably be the newest SBC from  [Pine64](https://www.pine64.org/). They will soon be releasing the [HardROCK64](https://www.hackerboards.com/product/410/) which should be the same price as the RPi4 and all around more performant, with socket for [eMMC modules](https://store.pine64.org/?product=32gb-emmc).

↰ [Return to Index](index.md)
