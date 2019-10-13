---
layout: post
title:  "Containers on ARM"
author: afbjorklund
---

# Containers on ARM

Now half-way through Hacktober, and again revisiting the task of
running containers on the [Raspberry Pi](https://www.raspberrypi.org/)
(which is using ARM CPU) instead of the usual `x86_64` virtual machine.

The initial focus is on the 32-bit models (`armv6l` and `armv7l`), with
the 64-bit version (`aarch64`) coming later. Currently a bit unstable,
but has a lot of interest server-side.

## Hardware

Here is a short summary of the available models of Raspberry Pi:

| #  | Arch  | Bits   | CPU | RAM
| ---| ----- | ------ | --- | ----
| 0  | `armv6` | 32-bit | x 1 | 512M
| 1  | `armv6` | 32-bit | x 1 | 512M
| 2  | `armv7` | 32-bit | x 4 | 512M
| 3  | `armv7` | 64-bit | x 4 | 1G
| 4  | `armv8` | 64-bit | x 4 | 1-4G

See also <https://en.wikipedia.org/wiki/Raspberry_Pi> for details.

## QEMU

Linux has a feature `binfmt_misc`, which allows the kernel to start a
program using any interpreter - such as for instance `qemu-arm`.

This allows us to run `armv6` containers on a regular `x86_64` kernel.
Unfortunately it is a bit unstable, _especially_ with Go programs...

## piCore

Tiny Core Linux has a version for the Raspberry Pi called "piCore".
The 9.x version has been released, but the 10.x is still in "beta".

<http://www.tinycorelinux.net/9.x/armv6>

This allows building an image, including `qemu-arm-static` for the
older kernels, as well as the armv6 rootfs from the piCore initramfs:

<https://github.com/boot2podman/boot2podman/tree/master/containers/tinycore-arm>

## Podman

The current work is about building a piCore with the features that are
required to run containers (cgroups and overlayfs).

Completed so far is building a Go compiler and building the packages
with the required software (like conmon and runc).
