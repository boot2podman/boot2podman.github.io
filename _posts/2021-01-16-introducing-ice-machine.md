---
layout: post
title:  "Introducing Ice Machine"
author: afbjorklund
---

# Introducing Ice Machine

Both `docker-machine` and `podman-machine` are now deprecated upstream,<br />
and not supporting the latest version of the container engines anymore.

The new **Floe** distribution will include a new simple version of `machine`,<br />
which will be called **Ice**. Initially it will support QEMU and VirtualBox.

<img alt="Ice Cubes" src="/assets/ice-cubes.png" />


It's a simplified version, that only supports the newer versions of the virtual machine.

And it will _only_ connect using SSH, so it doesn't need the old tcp tls certs or varlink.

```
Running pre-create checks...
Creating machine...
(box) Creating VirtualBox VM...
(box) Creating SSH key...
(box) Starting the VM...
(box) Check network to re-create if needed...
(box) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Machine is up and running!
```

Eventually it might add some simplified version of the remote cloud support, as well.

Expected to be available at the end of the month (Feb'21), after the FOSDEM conference.

## Floe

Replaces `boot2docker.iso` and `boot2podman.iso`, with a standard Linux distribution.

See [Introducing Floe Linux]({% post_url _posts/2021-01-10-introducing-floe-linux %})

----

Image credit: <a href="http://www.freepik.com">Designed by macrovector / Freepik</a>
