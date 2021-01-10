---
layout: post
title:  "Introducing Floe Linux"
author: afbjorklund
---

# Introducing Floe Linux

The [boot2docker](https://github.com/boot2docker) and [boot2podman](https://github.com/boot2podman) projects have been deprecated by their upstreams.

There is also a desire to have a _common_ container-capable "core" operating system...
Instead of having one OS distribution specific to each container runtime vendor.
The kernel and filesystems come prepared, and then the runtime comes from packages.
This makes the initial system small (16 MB), as originally intended by the upstream.
(i.e. **Tiny Core**)

Starting out on a new journey also means getting rid of some of the old legacy.
This will now use Linux version 5, and a 64-bit operating system (amd64/arm64).
Also focus on the new cgroup v2, rather than the previous cgroup v1 setup.
All connections will use unix sockets tunneled over ssh connections, not tcp.
But still build everything, **from source**.

Important filesystems:

* `squashfs`
* `cgroupfs`\*
* `overlayfs`\*

\* _requires custom kernel_

Three different variants:

* Linux (core / boot)
* Docker (docker.com)
* Podman (podman.io)

For more information, see:

<https://github.com/floelinux>

## Linux

Based on Tiny Core Linux, this has a Linux kernel and an initial RAM disk (initrd).

`$ tce-load -wi openssh`

Boot:

* isolinux
* vmlinuz
* initrd.img

Based on the CorePure64.iso (10.x)

<img alt="Ice Floe with Penguin" src="/assets/floe-penguin.png" />

## Docker

Adding support for the Docker container runtime, to the basic Floe installation.

`$ tce-load -wi docker`

Packages:

* runc.tcz
* containerd.tcz
* docker.tcz

Replaces the boot2docker.iso (19.03)

<img alt="Ice Floe with Whale" src="/assets/floe-whale.png" />

## Podman

Adding support for the Podman container runtime, to the basic Floe installation.

`$ tce-load -wi podman`

Packages:

* crun.tcz
* conmon.tcz
* podman.tcz

Replaces the boot2podman.iso (1.9.3)

<img alt="Ice Floe with Seal" src="/assets/floe-seal.png" />

## QEMU

Here showing the current upstream development version, TinyCoreLinux 12.0alpha1:

`$ kvm -cdrom boot.iso`

This will use a single processor (vCPU) and the default memory allocation (128 MB):

Like: `-smp 1 -m 128`

<img alt="QEMU Tiny Core Linux" src="/assets/qemutinycorelinux.png" />

A typical TCL system only runs the `init` process, and the udev and dhcp daemons:

```console
tc@box:~$ pstree -p
init(1)-+-sh(480)---pstree(557)
        |-udevd(119)-+-udevd(308)
        |            `-udevd(309)
        `-udhcpc(538)
```

Additional TCL features can be enabled, by using "boot codes" at the boot prompt:

```text
   ( '>')
  /) TC (\   Core is distributed with ABSOLUTELY NO WARRANTY.
 (/-_--_-\)           www.tinycorelinux.net

Press <Enter> to begin or F2, F3, or F4 to view boot options.
boot: corepure64 noembed
```

Now using `noembed`

> By default, Core uses the tmpfs setup by the kernel (rootfs); with this bootcode,<br />
> Core will setup a new tmpfs file system, and use that instead.

Container runtimes need to be able to call `pivot_root`, which doesn't work on rootfs:

See <https://www.kernel.org/doc/Documentation/filesystems/ramfs-rootfs-initramfs.txt>

> You can't unmount rootfs for approximately the same reason you can't kill the init
> process; rather than having special code to check for and handle an empty list, it's
> smaller and simpler for the kernel to just make sure certain lists can't become empty.

The only side effect is that the RAM memory usage _at boot_ will be doubled, i.e. 32 MB.

----

Image credit: <a href="http://www.freepik.com">Designed by upklyak / Freepik</a>
