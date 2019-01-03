---
title:  "Tiny init / Minimal (tini / mini)"
layout: post
author: afbjorklund
---

# Tiny init / Minimal (tini / mini)

## tinycore-tini

Tini - A tiny but valid init for containers

_See_ [https://github.com/krallin/tini](https://github.com/krallin/tini)

All Tini does is spawn a single child (Tini is meant to be run in a container),
and wait for it to exit all the while reaping zombies and performing signal forwarding.

> - It protects you from software that accidentally creates zombie processes,
>   which can (over time!) starve your entire system for PIDs (and make it
>   unusable).
> - It ensures that the *default signal handlers* work for the software you run
>   in your container image. For example, with Tini, `SIGTERM` properly terminates
>   your process even if you didn't explicitly install a signal handler for it.
> - It does so completely transparently! Container images that work without Tini
>   will work with Tini without any changes.

Showing virtual machine, running normal `init`:

``` console
   ( '>')
  /) TC (\   Core is distributed with ABSOLUTELY NO WARRANTY.
 (/-_--_-\)           www.tinycorelinux.net

tc@box:~$ pstree -p
init(1)-+-sh(473)---pstree(532)
        |-udevd(110)-+-udevd(289)
        |            `-udevd(334)
        `-udhcpc(531)
```

Showing container, running `tini`:

``` console
$ sudo podman run -it boot2podman-docker-tinycore.bintray.io/tinycore-tini:9.0-x86_64 sh
/ $ pstree -p
tini(1)---sh(8)---pstree(9)
```

As compared to without entrypoint:

``` console
$ sudo podman run -it boot2podman-docker-tinycore.bintray.io/tinycore:9.0-x86_64
/ $ pstree -p
sh(1)---pstree(8)
```

Ideally, this would be something like:

``` Dockerfile
RUN tce-load -wic tini.tcz \
    && rm -rf /tmp/tce/optional/*
ENTRYPOINT ["/usr/local/sbin/tini", "--"]
```

## tinycore-mini

This is a minimal container, consisting only of the standard C library and linker:

``` txt
/lib/libc.so.6
/lib/ld-linux-x86-64.so.2
```

Unlike the normal 8M container, there's **no** shell included (not even `/bin/sh`)

``` txt
starting container process caused "exec: \"sh\": executable file not found in $PATH"
```

Allows for really small (10k) containers, when based on the 2M parent image:

``` txt
ID             CREATED             CREATED BY                               SIZE      COMMENT
62a66b04e762   25 minutes ago      /bin/sh -c #(nop) CMD ["/bin/hello"]     1.024kB   
a92252aa9346   25 minutes ago      /bin/sh -c #(nop) ADD hello /bin/hello   10.24kB   
a9e530ddf4e1   About an hour ago   /bin/sh -c #(nop) ADD minimal.tar.gz /   1.73MB    
```

Static linking (rather than dynamic) also works, but then each binary is bigger

``` txt
8.0K	hello
616.0K	hello-static
```

## Source

See [https://github.com/boot2podman/boot2podman/tree/master/containers](https://github.com/boot2podman/boot2podman/tree/master/containers)
