---
layout: post
title:  "Hacktober Season"
author: afbjorklund
---

# Hacktober Season

This year is a bit special, and it also started on the wrong foot...<br />
Some people are trying to _spam_ their way into getting a T-shirt!

Talk about missing the point, you can read more about the event on:

<https://hacktoberfest.digitalocean.com/>

## Vagrant Machine

There will be a drop-in replacement for the discontinued Docker Machine<br />
and Podman Machine projects, the working title is `vagrant-machine`.

```
$ vagrant-machine create
$ vagrant-machine env
```

See [Machine Replacement]({% post_url 2020-07-22-machine-replacement %})

## Buildroot Changes

I split previous virtual images into one for Docker (booting from ramdisk)<br />
and one for Kubernetes (booting from disk, just like the Raspberry Pi images)

```
72M	output/buildroot.iso
143M	output/disk.img.gz
```

See [Proof-of-Concept Release]({% post_url 2020-07-10-proof-of-concept-release %})

## NVIDIA GTC 2020

Will again join the GPU Technology Conference, excited about NVIDIA and ARM.

_Oct 5 - 9_

<https://www.nvidia.com/en-us/gtc/>

## KubeCon '20 NA Virtual

Going straight for Slack and YouTube this time, same "sleepy" 12:00 schedule.

_Nov 17 - 20_

<https://events.linuxfoundation.org/kubecon-cloudnativecon-north-america/>
