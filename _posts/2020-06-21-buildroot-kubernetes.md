---
layout: post
title:  "Buildroot Kubernetes"
author: afbjorklund
---

# Buildroot Kubernetes

Buildroot is a simple, efficient and easy-to-use tool to generate embedded Linux systems through cross-compilation.

<https://buildroot.org/>

It comes with very nice documentation, and is updated in yearly Long Term Support (LTS) releases (latest being 2020.02.x).

Used for minikube.iso

## Several possibilities

When integrating a system, there are several possibilities:

> * Building everything manually
>
> * Binary distribution
>
> * Build systems

There are pros and cons of each, as described nicely here:

<a href="/assets/buildroot-possibilities.pdf"><img alt="buildroot possibilities" src="/assets/buildroot-possibilities.png" width="100%" /></a>

_Taken from the Buildroot documentation which is: (c) Copyright 2004-2020, Bootlin_

<https://bootlin.com/training/buildroot/>

## Distribution

The boot2podman integration is a mix of manual build and binary distribution:

* Tiny Core Linux <http://tinycorelinux.net/>
* Container kernel and packages

Many of the packages are custom-made from source, in _Linux From Scratch_ fashion.

Compared to something like hypriot, which is a more of a traditional distribution:

* Raspbian (Debian) <http://raspbian.org/>
* Container kernel and packages

But using a build system like Buildroot integrates the best of both of the other two.

You get high-level packaging and code re-use by using simple `make` based system.
And you also get host tools and cross-compilation, instead of having to use target.

The major down side is that there is no runtime package manager, only buildtime.

## Kubernetes

Building on boot2docker, adding systemd and kubeadm into **buildroot4kubernetes**.

We still need the kernel container support (namespaces, cgroups, overlayfs).
But now also some advanced networking support (nat, bridge, conntrack, vxlan).

The simple `init` system is replaced with the more complex `systemd` platform.

There are still the docker programs (dockerd, containerd, docker).
But now also with the kubernetes programs (kubeadm, kubelet, kubectl).

<https://github.com/afbjorklund/buildroot4kubernetes>

There are two major configuration files used:

* `buildroot_defconfig`

* `kernel_defconfig`

Both using the [Kconfig](https://www.kernel.org/doc/html/latest/kbuild/) configuration system, originally from the Kernel Build System.

This produces two things as the build output:

* Linux kernel image

* Root file system

These two files then get bundled into a bootable CD image or a flashable SD image, depending on the platform.

### X86

* `amd64` (x86\_64)

For running with QEMU/KVM and other hypervisors:

```
126M	output/buildroot.iso
```

### ARM

* `arm64` (aarch64)

For flashing for Raspberry Pi 3 and later models:

```
127M	output/sdcard.img.zip
```

### cri-o

It would be possible to do an image version replacing docker with podman
and containerd with cri-o, ibut using the same kernel and other packages.

### k3s

The actual Kubernetes (k8s) installation is done using container images,
making this installation around three times bigger total than using k3s.

## Others

The reference installation, based on Ubuntu and the official Google packages,
can be found for instance here. Using Vagrant and Ansible, for simplicity.

<https://github.com/afbjorklund/vanilla-kubernetes>

A supported and ready-to-run solution is available in the Minikube project.
It also uses Buildroot, but has more packages added beyond the minimal.

<https://github.com/kubernetes/minikube>
