---
layout: post
title:  "Updated Images"
author: afbjorklund
---

# Updated Images

Now that a long-standing bug in Podman 1.5 and 1.6 has been fixed,<br>
it is easier to update the images again (the builds are using podman).

## Boot2Podman v0.26

`boot2podman.iso` (117M)

- Podman 1.7 (<https://podman.io>)
- Buildah 1.14 (<https://buildah.io>)

`boot2podman-kubernetes.iso` (227M)

- CRI-O 1.17 (<https://cri-o.io>)
- K3S 1.17 (<https://k3s.io>)

<https://github.com/boot2podman/boot2podman/releases/tag/v0.26>

## Relationship

As was described in [three sizes]({% post_url 2019-06-09-three-sizes %}),
all images are sharing the base.

The image layers are: corepure64 < boot2podman < kubernetes

## Kubernetes

See [lightweight kubernetes]({% post_url 2019-03-31-lightweight-kubernetes %})
for more information about this.

The `crio` service is started by default, but `k3s` is manual.
