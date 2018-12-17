---
title:  "Boot2Podman and Kubernetes"
layout: post
author: afbjorklund
---

# Boot2Podman and Kubernetes

The tools `podman-machine` and `boot2podman.iso` are intended for running
virtual machines locally, but not for running node clusters or remotely.
For that purpose, one is better off running `minikube` and `minikube.iso`
(or even `kubeadm` directly in cloud).

Both projects are using the same [runc](https://runc.io/) project for
running containers, with [cri-o](https://cri-o.io/) doing the runtime
monitoring of containers for Kubernetes. See: minikube --container-runtime=cri-o
(this task is normally instead handled by the smaller `conmon` program, in Podman)

## Machine

You can have multiple machines, but each node have its isolated containers.
The containers/pods are accessed using SSH to reach the machine and varlink.

Normally you run containers, but you can group your containers into pods.
Access control is handled by normal file permissions to the files or socket.

## Kubernetes

You can have multiple nodes, and the master will orchestrate between them.
The containers/pods are controlled using HTTP to contact the k8s REST API.

Normally you run pods, but each pods consists of one or more containers.
Access control is handled by admin authentication using configuration.

# Minikube

There are currently some remaining issues, when using CRI-O runtime:

[https://github.com/kubernetes/minikube/issues/3296](https://github.com/kubernetes/minikube/issues/3296)

But the goal of Kubernetes is to make it possible to use **all** runtimes:

[https://kubernetes.io/docs/setup/cri/](https://kubernetes.io/docs/setup/cri/)

# Kubeadm

Switching the container runtime to CRI-O requires some configuration:

[https://github.com/kubernetes-sigs/cri-o/blob/master/kubernetes.md](https://github.com/kubernetes-sigs/cri-o/blob/master/kubernetes.md)

You also need to install and start the CRI-O container runtime service:

[https://github.com/kubernetes-sigs/cri-o](https://github.com/kubernetes-sigs/cri-o)

# Open Container Initiative

Both Podman and Kubernetes are running standard [OCI](https://www.opencontainers.org/) Linux containers.

This involves the OCI Image specification and OCI Runtime specification.

## CRI

Container Runtime Interface, used by Kubernetes since v1.6.0

## CNI

Container Network Interface, used by both Podman and Kubernetes
