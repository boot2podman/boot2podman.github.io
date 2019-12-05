---
layout: post
title:  "Minikube Presentation"
author: afbjorklund
---

# Minikube Presentation

I held a presentation on the Kubernetes Göteborg ([Cloud Native Nordics](https://www.cloudnativenordics.com/))<br>
meetup that was generously hosted by Meltwater, Wed December 4th, 2019.

<https://www.meetup.com/Kubernetes-Goteborg/events/265686037/>

The theme of the evening was Local Kubernetes, and I presented Minikube<br>
and some Machine history and upcoming features like KIC and Multinode.

There were also presentations of KIND and of k3s (running with Multipass)<br>
A very nice evening, and the three projects had lots of things in common.

Unfortunately, the video recording equipment did not want to cooperate...

## Related Projects

As was mentioned in the presentation, Minikube runs Kubernetes.

Another way to install Kubernetes is to use Vagrant and Ansible:

<https://github.com/afbjorklund/vanilla-kubernetes>

This is the most basic flavour of k8s, using Ubuntu and Docker.

Also mentioned in the presentation, k3s is similar to localkube:

<https://github.com/afbjorklund/docker-machine-minikube-install>

But it supports newer Kubernetes versions, and is even smaller!

<https://github.com/afbjorklund/docker-machine-k3s-install>

## Previous Presentations

* [Boot2podman Kubernetes]({% post_url 2019-04-09-boot2podman-kubernetes %})

* [Containers without Docker]({% post_url 2019-02-19-containers-without-docker %})

----

Slides: [MinikubePresentation.pdf](/assets/MinikubePresentation.pdf)
