---
layout: post
title:  "Proof-of-Concept Release"
author: afbjorklund
---

# Proof-of-Concept Release

The early releases from the "buildroot4kubernetes" project are up:

<https://github.com/afbjorklund/buildroot4kubernetes>

* `amd64` (qemu_x86_64)
* `arm64` (raspberrypi3_64)

## Release Files

amd64:
`buildroot.iso`
`images.iso`

arm64:
`sdcard.img.zip`
`images.tar.gz`

## Components

It is similar to "boot2docker", but also adds kubernetes components:

* Docker engine (`dockerd`)
* Docker containerd (`containerd`)
* Docker client (`docker`)

* Kubernetes installer (`kubeadm`)
* Kubernetes service (`kubelet`)
* Kubernetes client (`kubectl`)

* CRI Container Runtime Interface tools (`crictl`)
* CNI Container Network Interface plugins (`/opt/cni`)

## Docker Images

Everything else is run from containers, after the initial bootstrap:

* kube-controller-manager
* kube-apiserver
* etcd
* kube-scheduler
* kube-proxy
* coredns

There is also a default CNI plugin included, "flannel" (using VXLAN).

* flannel

As well as the special "infra" container which is used by the k8s pods.

* pause

## Usage

The idea is that the user should have just enough to bootstrap Kubernetes...

Either a new control plane (`kubeadm init`) or a worker (`kubeadm join`):

* <https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init/>

* <https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-join/>

If wanting to deploy the network plugin, there are some extra steps needed:

```sh
kubeadm init --pod-network-cidr=10.244.0.0/16

export KUBECONFIG=/etc/kubernetes/admin.conf
kubectl apply -f /etc/kubernetes/flannel.yml
```

You could also use a different network plugin, see [kubeadm documentation](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#pod-network)

* Canal <https://github.com/projectcalico/canal>
* Calico <https://github.com/projectcalico/calico>
* Weave <https://github.com/weaveworks/weave>

## Differences

These are the biggest differences to boot2podman kubernetes:

* Buildroot (instead of Tiny Core Linux)
* Systemd (instead of `init(1)` and cgroupfs)
* Raspberry Pi support (in addition to KVM)

* docker (instead of podman)
* containerd (instead of cri-o)
* kubernetes/k8s (instead of k3s)

This was described further in some earlier posts on the topic:

* [Buildroot Kubernetes]({% post_url 2020-06-21-buildroot-kubernetes %})

* [Lightweight Kubernetes]({% post_url 2019-03-31-lightweight-kubernetes %})

## Future

Some future development paths to be investigated further:

* Raspberry Pi Zero (`armv6`)

* Administration (like "machine")