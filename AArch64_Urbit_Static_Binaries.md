---
title: AArch64 Urbit Static Binaries
description: Already compiled static binaries for Urbit on AArch64
---

↰ [Return to Index](index.md)

# AArch64 Urbit Static Binaries

These binaries have been placed into an [APT repository](Urbit_AArch64_APT_Repository.md) for easy installation and upgrades on debian derived linux distributions.

Available from [my Urbit github fork](https://github.com/botter-nidnul/urbit/releases/tag/urbit-v1.1-aarch64).

If you use these on Raspbian you will still have to follow *Step One: Kernel* from [Steps to Urbit on Raspberry Pi](Steps_to_Urbit_on_Raspberry_Pi.md) but the rest of that guide *can* be ignored (though you *shouldn't* ignore [Step Seven](Steps_to_Urbit_on_Raspberry_Pi.md#step-seven-configure-trim-timer)).

```
curl -OL https://github.com/botter-nidnul/urbit/releases/download/urbit-v1.1-aarch64/urbit-v1.1-c841f.tar.gz
tar xzf urbit-v1.1-c841f.tar.gz
./urbit-v1.1-aarch64-linux/urbit sampel-palnet
```

↰ [Return to Index](index.md)
