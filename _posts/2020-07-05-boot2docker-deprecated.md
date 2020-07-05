---
title: "Boot2Docker Deprecated"
layout: post
author: afbjorklund
---

# Boot2Docker Deprecated

The boot2docker project has announced, that v19.03.12 will be the _final_ release:

<https://github.com/boot2docker/boot2docker/pull/1408>

> Boot2Docker is officially deprecated and unmaintained. It is recommended that
> users transition from Boot2Docker over to Docker Desktop instead (especially
> with the new WSL2 backend, which supports Windows 10 Home).

A similar announcement was made earlier in 2018, for the docker-machine project:

<https://github.com/docker/machine/issues/4537>

> As has been obvious for some time now, we've slowly stopped implementing or
> accepting new features for the project. Its desktop usage has mostly been
> supplanted by our Docker Desktop product.


## Boot2Podman

For the boot2podman project, there are two other things that are more impacting.

* OpenShift v4 has replaced the Fedora/CentOS image with a Fedora CoreOS image
  This means that there is less maintenance going into the alternative image base

* Podman v2 has replaced the varlink API with a new rest API instead (still SSH)
  This makes it more compatible with Docker, but less compatible with Podman v1

There are also the upcoming changes for Cgroups V2, as well as rootfs and cgroupfs.

## Tiny Core

The upstream [Core project](http://tinycorelinux.net/) is still going strong, and is not really going anywhere...

It might be possible to provide support for docker and podman as .tcz packages only.
However, to _use_ them you would need to use a Linux kernel with container support.

Alternative projects such as [Debian Live](https://www.debian.org/CD/live/) is currently showing a much larger footprint,
the download being almost 100x bigger. But it can be done, as shown by HypriotOS.

## Replacements

Boot2Docker says "there are a lot of tools designed to help spin up environments"
and Docker says to use `DOCKER_HOST` with `ssh://` instead of using Docker Machine.

Which basically means that the poor user is left to the situation that was before,
unless they want to go with **Docker Desktop** or **Red Hat CodeReady Containers** instead.

It goes a little something like this:
1. Start a machine, install an OS
2. Install Docker Community Edition
3. Configure access and certificates

Products:

* Vagrant: <https://www.vagrantup.com/docs/provisioning/docker.html>

* Docker: <https://www.docker.com/products/docker-desktop> (Win and Mac)

* Red Hat: <https://developers.redhat.com/products/codeready-containers>

## Future Development

The current projects will still be available, for Docker 19.03 and for Podman 1.9.3.<br />
But there might **not** be any more future releases, for Docker 20.x or Podman 2.0.x

There will be a final release on the existing roadmap for Boot2Podman as announced,<br />
but most likely development will switch to using Buildroot and Kubernetes instead.

----

"So Long, and Thanks for All the Fish"

_-- Douglas Adams_

