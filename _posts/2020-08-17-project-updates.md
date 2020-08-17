---
layout: post
title:  "Project Updates"
author: afbjorklund
---

# Project Updates

## Boot2Podman deprecated

With Boot2Docker deprecated and not too much interest in just Podman,<br>
there will be no more update of podman-machine - beyond using Vagrant.

* [Machine Replacement]({% post_url 2020-07-22-machine-replacement %}) - beyond `v1.9.3`

## Raspberry Pi Kubernetes

Evaluated running kubernetes on armv6, and it isn't feasible anymore...<br>
So no more Rpi1. Will run k3s on the Rpi2, and k8s on the Rpi3 and up.

<https://www.raspberrypi.org/blog/five-years-of-raspberry-pi-clusters/>

## Booting, from CD to HD

Now when not using Tiny Core Linux anymore, things don't fit into RAM.<br>
So do a regular hard drive install, instead of the "Live CD" and squashfs.

* [Proof-of-Concept Release]({% post_url 2020-07-10-proof-of-concept-release %}) - now at `v0.13`

## KubeCon '20 EU Virtual

It seems like Slack and YouTube is where the conferences are happening.<br>
There is some old "conference platform", but it doesn't seem to add much.

<https://events.linuxfoundation.org/kubecon-cloudnativecon-europe/>
