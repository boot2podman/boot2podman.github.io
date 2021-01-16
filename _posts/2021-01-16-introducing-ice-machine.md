---
layout: post
title:  "Introducing Ice Machine"
author: afbjorklund
---

# Introducing Ice Machine

Both `docker-machine` and `podman-machine` are deprecated upstream, and not supporting the latest.

The new Floe distribution will include a new simple version of `machine`, which will be called Ice.


Basically it's a simplified version, that only supports the newer versions of the virtual machine.

And it will _only_ connect using SSH, so it doesn't have the old complications of certs or varlink.


Expected to be available at the end of the month (Feb'21), after the FOSDEM conference.

See [Introducing Floe Linux]({% post_url _posts/2021-01-10-introducing-floe-linux %})
