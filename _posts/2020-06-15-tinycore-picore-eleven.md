---
layout: post
title:  "Tiny Core and piCore 11.x"
author: afbjorklund
---

# Tiny Core Linux 11.1

The first update to Tiny Core 11.x is out, release notes on the [tinycore forum](http://forum.tinycorelinux.net/index.php/topic,23692.0.html)

Kernel: 5.4.3

As usual there are `x86` and `x86_64`, but we only care about the 64-bit.

``` txt
16M     CorePure64-11.1.iso
```

# piCore 11.0 (armv7l)

Also the first update since piCore 9.0 (2017), was released on [tinycore forum](http://forum.tinycorelinux.net/index.php/topic,23935.0.html)

Kernel: 4.19.81

There is no 64-bit `aarch64` version yet, but still very good news indeed.

``` txt
89M     piCore-11.0.zip
```

## Raspberry Pi variants

Note that the Raspberry Pi model 3 and 4 actually have an ARMv8-A CPU.

But currently piCore (and Raspbian) runs the more compatible 32-bit.

piCore

RPi | Arch    | Kernel            | Flags
--- | ------- | ----------------- | ------------------------
0-1 | `armv6` | bcmrpi_defconfig  | CFLAGS="-march=armv6zk -mtune=arm1176jzf-s -mfpu=vfp"
2-3 | `armv7` | bcm2709_defconfig | CFLAGS="-mcpu=cortex-a7"
4   | `armv7l`| bcm2711_defconfig | CFLAGS="-mcpu=cortex-a7"

Source: <https://www.raspberrypi.org/documentation/linux/kernel/building.md>

CFLAGS

Board          | GCC optimisation flags
-----          | ----------------------
Raspberry Pi 1 | `-mcpu=arm1176jzf-s -mfloat-abi=hard -mfpu=vfp` (alias for vfpv2)
Raspberry Pi 2 | `-mcpu=cortex-a7 -mfloat-abi=hard -mfpu=neon-vfpv4`
Raspberry Pi 3 | `-mcpu=cortex-a53 -mfloat-abi=hard -mfpu=neon-fp-armv8 -mneon-for-64bits`
Raspberry Pi 4 | `-mcpu=cortex-a72 -mfloat-abi=hard -mfpu=neon-fp-armv8 -mneon-for-64bits`

Source: [gcc compiler optimization for arm systems.md](https://gist.github.com/fm4dd/c663217935dc17f0fc73c9c81b0aa845)
