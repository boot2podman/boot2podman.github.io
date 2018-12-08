---
title:  "Fedora ISO Variant"
layout: post
author: afbjorklund
---

# Boot2Podman Fedora ISO

The regular `boot2podman.iso` is based on [Tiny Core Linux](http://tinycorelinux.net/):

[https://github.com/boot2podman/boot2podman](https://github.com/boot2podman/boot2podman)

There is now an alternative version, based on [Fedora Linux](https://getfedora.org/):

[https://github.com/boot2podman/boot2podman-fedora-iso](https://github.com/boot2podman/boot2podman-fedora-iso)

Both versions will do the same thing, in that they will both offer the Podman varlink socket.

The [Podman Machine](https://github.com/boot2podman/machine) can set up virtual machines for either, by using the "url" parameters.

## Tiny Core

This is a minimal system, that runs entirely from RAM and uses `init(1)`.

The package manager uses TCZ packages, handled by the `tce-load` program.

The currently used version is CorePure64 (9.x)

_See:_ [https://en.wikipedia.org/wiki/Tiny_Core_Linux](https://en.wikipedia.org/wiki/Tiny_Core_Linux)

## Fedora

This is a full system, that boots a regular image and uses `systemd(1)`.

The package manager uses RPM packages, handled by the `dnf` program.

The currently used version is Fedora (28)

_See:_ [https://en.wikipedia.org/wiki/Fedora_(operating_system)](https://en.wikipedia.org/wiki/Fedora_(operating_system))

## Others

There are some other similar projects, not yet supported by `podman-machine`.

Most are intended for clusters and Kubernetes, rather than just running Podman.

### Minikube

This is a Linux distribution made with **BuildRoot**, and offers `machine` compatibility.

_See:_ [https://kubernetes.io/docs/setup/minikube/](https://kubernetes.io/docs/setup/minikube/)

### Minishift

Similar to `minikube`, but intended for running **OpenShift** rather than **Kubernetes**.

_See:_ [https://docs.okd.io/latest/minishift/getting-started/](https://docs.okd.io/latest/minishift/getting-started/)

### CoreOS

One alternative to these, is **Container Linux**, from [CoreOS](https://coreos.com/).

_See:_ [https://en.wikipedia.org/wiki/Container_Linux_by_CoreOS](https://en.wikipedia.org/wiki/Container_Linux_by_CoreOS)

### Atomic

Another alternative is **Atomic Host**, from [Project Atomic](https://www.projectatomic.io/).

_See:_ [http://www.projectatomic.io/docs/introduction/]( http://www.projectatomic.io/docs/introduction/) ([Fedora](https://getfedora.org/en/atomic/))

## Fedora CoreOS

> Fedora CoreOS is an automatically updating, minimal, monolithic, container-focused operating system,
> designed for clusters but also operable standalone, optimized for Kubernetes but also great without it.
>
> It aims to combine the best of both CoreOS Container Linux and Fedora Atomic Host

Eventually it will appear at [https://coreos.fedoraproject.org/](https://coreos.fedoraproject.org/)