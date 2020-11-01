---
layout: post
title:  "Remember November"
author: afbjorklund
---

# Remember November

> Remember, remember the fifth of November<br />
> Gunpowder, treason and plot.<br />
> I see no reason, why gunpowder treason<br />
> Should ever be forgot.<br />

Now that Hacktober is over (maybe for good this time, due to the spam), <br />
seems like a good time to end the deprecated "boot2podman" projects...

Will be holding a project retrospective on the Podman Community Meeting,<br />
and announce the new name on the "CloudNativeGbg" meetup on the 5th.

## OS Alternatives

### Vagrant

* "Machine" - replacement for docker-machine and podman-machine
* "Minikube" - setup for running wth the "generic" ssh minikube driver

_just the standard Ubuntu/Docker and Fedora/Podman images_

### Buildroot

* "Docker" - booting Docker from ramdisk with init (75M)
* "Kubernetes" - Kubernetes from disk with systemd (150M*)

\* _`kubeadm` only, excluding the necessary container images_

Not using the bespoke custom OS, based on Tiny Core Linux, anymore.<br />
But rather standard Linux distributions - whether from binary or source.

The footprint doubles, but it does make maintenance and support easier.<br />
And makes it easier to target new platforms, such as the ARM architecture.

## Living on the Edge

Made a presentation about the Raspberry Pi and the Jetson Nano

See [At the Edge Presentation]({% post_url 2020-10-07-at-the-edge-presentation %})

Attended the conference from SUSE and Rancher about k3s and cri-o

<https://edgeconference.io/>

Just going with the standard k8s and docker / moby software for now,<br />
but maybe will get back to k3s for the smaller footprint deployments.

Not sure why to use podman and cri-o instead of docker and containerd,<br />
currently it doesn't seem worth it - unless you are Red Hat or SUSE...

## Virtual Conferences

### FOSS North, Take II

_Nov 1_

<https://foss-north.se/2020ii/>

### All Day DevOps (ADDO)

_Nov 12_

<https://www.alldaydevops.com/>

### KubeCon+CloudNativeCon

_Nov 17 - 20_

[https://www.cncf.io/events/](https://www.cncf.io/events/kubecon-cloudnativecon-north-america-2020/)

### FOSDEM 2021 (Online)

_Feb 6 - 7_

<https://fosdem.org/2021/>
