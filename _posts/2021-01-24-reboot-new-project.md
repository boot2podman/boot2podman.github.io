---
layout: post
title:  "Reboot: New Project"
---

# Reboot: New Project

As posted earlier, the "boot2podman" project is deprecated:

* [Boot2Podman Project]({% post_url 2020-11-03-boot2podman-project %})
* ~~<https://github.com/boot2podman>~~

The original "boot2docker" project has also been deprecated:

* [Boot2Docker Deprecated]({% post_url 2020-07-05-boot2docker-deprecated %})
* ~~<https://github.com/boot2docker>~~

But my work will continue, at the new: <https://floelinux.github.io>

It will also include a `machine`... With support for **both** runtimes.

## Floe boot sequence video

Here is the basic boot sequence of the new Core system (6s):

<video controls="controls" width="736" height="416">
    <source src="/assets/floe.webm" type="video/webm">
</video>

After the boot is complete, individual TCE packages can be loaded:

* `openssh.tcz`
* `docker.tcz`
* `podman.tcz`

And the container runtimes can be started, just like it was previously...

## Fresh Start

This means that development can continue, without being tied to<br />
one specific company (like Docker Inc, or Red Hat) and one runtime.

Instead the same basic system can be used for multiple projects.<br />
It also keeps the Tiny Core a _lot_ smaller, currently it is 16 - 24 MB.

The packages are mounted (squashfs) from disk, as originally intended.<br />
Instead of being copied to the RAM file system, like it was previously.

You can also run the Core system _itself_ as a container, e.g. for builds.<br />
There is no support for doing mounts, but one can use volumes instead.

## New Features

* Linux 5.4
* GCC 9.2
* Go 1.15
* Docker 20.10
* Podman 2.1+
* SSH socket

## More Info

For more information, see:

* [Introducing Floe Linux]({% post_url 2021-01-10-introducing-floe-linux %})
* [Introducing Ice Machine]({% post_url 2021-01-16-introducing-ice-machine %})
