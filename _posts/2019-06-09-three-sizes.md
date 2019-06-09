---
layout: post
title:  "Three Sizes of Image"
author: afbjorklund
---

# Three Sizes of Image

The bootable ISO file consists of two major components, the kernel and the filesystem.

The upstream image loads all modules and packages from the network, making it _tiny_:

[CorePure64-10.0.iso](http://www.tinycorelinux.net/10.x/x86_64/release/CorePure64-10.0.iso)

Size: 15M

<img alt="ISOLINUX boot menu" src="/assets/isolinux.png" width="100%" />

## Contents

Besides the Linux kernel (`vmlinuz64`), there are three images (`initrd`) in /boot:

* corepure64.gz
* boot2podman.gz
* kubernetes.gz

These are stacked into the actual memory filesystem, using the boot configuration.

They are all stand-alone, in that they don't require any further network download.

### corepure64

The "corepure64" image is same as in Tiny Core Linux, with some minor modifications. [^1]

[^1]: support has been added for cgroupfs and overlayfs, in order to run linux containers

The kernel itself is not so big, but includes a lot of kernel modules that take up space:

Size: 35M = 5M + 30M

### boot2podman

The "boot2podman" image adds all the packages needed to run Podman and Buildah. [^2]

[^2]: as usual the packages are provided in the .tcz format, which is mounted at runtime

Since most of them are statically linked, they take up twice as much as the base OS:

Size: 105M = 5M + 30M + 70M

### kubernetes

The "kubernetes" image adds packages/images required to run Kubernetes with CRI-O.

By k3s combining functions into one binary and switching database, it still kept small:

Size: 175M = 5M + 30M + 70M + 70M

----

See: <https://github.com/boot2podman/boot2podman/blob/master/remastering_tc.md>
