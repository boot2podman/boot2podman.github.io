---
layout: post
title:  "Lightweight Kubernetes"
author: afbjorklund
---

# Lightweight Kubernetes

Back in the old days (2017, Kubernetes 1.8) you could run `localkube` on boot2docker.

Since, minikube has moved to use `kubeadm` and a custom OS image based on coreos.

This unfortunately meant resource requirements doubled, even if it is more "compatible".

Now, there's a new [k3s](https://k3s.io/) distribution that is a perfect match with [cri-o](https://cri-o.io/) and boot2podman...

## cri-o

Lightweight container runtime for Kubernetes

<https://cri-o.io/>

## k3s

Lightweight Kubernetes. "5 less than k8s".

<https://k3s.io/>

## boot2podman

From initial testing, it will be possible to include **Kubernetes** with the `boot2podman.iso`.

The Kubernetes install (crio/k3s) is same size as the Podman install (podman/buildah) !

## Source

See <https://github.com/boot2podman/boot2podman/blob/master/building_kubernetes.md>
