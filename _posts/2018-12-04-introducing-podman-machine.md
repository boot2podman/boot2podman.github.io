---
title:  "Introducing Podman Machine"
layout: post
author: afbjorklund
---

# Introducing Podman Machine

The command-line tool `podman-machine` is a simple way to create virtual machines running `boot2podman.iso`.
It will create a "machine" with Linux prepared for running Linux containers, with [Podman](https://podman.io) and [Buildah](https://buildah.io) (and their dependencies) pre-installed.

This way any client will be able to run containers, even though not possible on their operating system.
Whether their Linux distribution is too old or too unprivileged, or if they are running Windows or Mac OS X operating systems without native Linux support.

## Podman Machine

Machine lets you create servers with Podman, then configures the Podman clients.

``` console
$ podman-machine create box
$ podman-machine ssh box

tc@box:~$ sudo podman version
```

Will automatically download the latest version of the ISO, if not available in the cache.

_See:_ [https://github.com/boot2podman/machine](https://github.com/boot2podman/machine)

## Boot2Podman ISO

Boot2podman is a lightweight Linux distribution made specifically to run Linux containers.

* Tiny Core Linux 9.x (x86_64)
* Buildah / Varlink / Podman

The distribution runs entirely from RAM, while persisting the containers and ssh keys.

_See:_ [https://github.com/boot2podman/boot2podman](https://github.com/boot2podman/boot2podman)

## Remote Access

It is possible to use the `pypodman` commmand-line tool, to control podman remotely:

``` console
$ eval $(podman-machine env box)
$ pypodman version
```

_See:_ [https://github.com/containers/libpod/tree/master/contrib/python](https://github.com/containers/libpod/tree/master/contrib/python)

Or alternatively to use the `varlink` command-line tool, to access the podman API:

``` console
$ eval $(podman-machine env box --varlink)
$ varlink call io.podman.GetVersion
```

_See:_ [https://github.com/varlink/libvarlink/tree/master/tool](https://github.com/varlink/libvarlink/tree/master/tool)

Both methods use SSH, in order to access the podman varlink socket of the VM.

The SSH keys and other configuration is automatically created with the machine.
