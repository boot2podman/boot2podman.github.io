---
layout: post
title:  "Three Sizes of Cluster"
author: afbjorklund
---

# Three Sizes of Cluster

The boot2podman distribution is focused on running containers on a single node.

But if you want to run a local cluster of nodes, here are some different form factors:

* Small
* Smaller
* Smallest

## Kubernetes

The idea here is to have one control plane node, and from one to three worker nodes:

![kubernetes architecture](/assets/kubernetes-architecture.png)

Source: <https://kubernetes.io>

The nodes will all run Kubernetes, which will talk to the container runtime (or "engine").

It is installed using `kubeadm`, a tool to bootstrap a minimum viable Kubernetes cluster.

## Small

Running virtual machines is the easiest way to set up a local cluster.<br />
This runs the same architecture as the regular laptop or public cloud.

QEMU/KVM on NUC
* 2GB RAM per node
* Architecture: `amd64`

£ 441.97 ($555) - _including cpu and memory_
* 1 x Intel NUC 10 Kit, Frost Canyon, Core i5 @ £369.98
* 2 x 8GB Corsair Vengeance DDR4 SODIMM 2400MHz @ £71.99

<img alt="Intel NUC 10" src="/assets/nuc_10.jpg" width="480" />

<https://www.redhat.com/en/topics/virtualization/what-is-virtualization>

<https://www.intel.com/content/www/us/en/products/boards-kits/nuc.html>

Note: need to add a disk as well, either M.2 SSD or 2.5" HDD.

## Smaller

The third generation introduced a more server-like 64-bit processor.<br />
Many cloud providers use these as a low-cost  / low-power alternative.

Raspberry Pi 3B
* 1GB RAM per node
* Architecture: `arm64`

£ 148.00 ($184) - _boards and case only_
* 2 x Cluster Case for Raspberry Pi (with Fans) @ £10.00
* 4 x Raspberry Pi 3 Model B @ £32.00

<img alt="Raspberry Pi 3 Cluster" src="/assets/rpi_3b.jpg" width="480" />

<https://thepihut.com/collections/raspberry-pi-store>

Note: Need to add a SD card for each, and power and network.

## Smallest

The credit-card sized version Zero of the single-board ARM computer.<br />
Now also has wireless support (both WiFi networking and Bluetooth)

Raspberry Pi 0W
* 512M RAM per node
* Architecture: `armv6`

£ 31.60 ($39) - _boards and case only_
* 1 x Mini Cluster Case for Raspberry Pi Zero @ £6.00
* 2 x Raspberry Pi Zero WH @ £12.80

<img alt="Raspberry Pi 0 Cluster" src="/assets/rpi_0w.jpg" width="480" />

<https://thepihut.com/collections/raspberry-pi-store>

Note: Need to add a SD card for each, and power (no network).

----

This new post was about the hardware, see the previous post for the software:

* [Buildroot Kubernetes]({% post_url 2020-06-21-buildroot-kubernetes %})

You can also run "system containers" instead of virtual machines or bare metal.

These are not included here, but do see [OpenVZ](https://openvz.org/) or [LXC](https://linuxcontainers.org/) for more information.

