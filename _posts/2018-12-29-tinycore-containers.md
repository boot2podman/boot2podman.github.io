---
title:  "TinyCore Containers"
layout: post
author: afbjorklund
---

# TinyCore Containers

The standard way of running is using the ISO on a physical server or virtual machine:

``` sh
wget http://www.tinycorelinux.net/9.x/x86_64/release/CorePure64-9.0.iso
qemu-system-x86_64 -cdrom CorePure64-9.0.iso
```

This will start the normal "isolinux" boot process, including starting another kernel.

       ( '>')
      /) TC (\   Core is distributed with ABSOLUTELY NO WARRANTY.
     (/-_--_-\)           www.tinycorelinux.net

    Press <Enter> to begin or F2, F3, or F4 to view boot options.
    boot:

And that works fine, virtualization can be hardware-accelerated with KVM (or similar)

``` console
$ kvm-ok
INFO: /dev/kvm exists
KVM acceleration can be used
```

But when building packages and cross-compiling, it can be useful to run in a container...

## cc

The [Tiny Core Linux](http://tinycorelinux.net) distribution is also available as a standard OCI container image:

``` console
$ sudo podman run -it boot2podman-docker-tinycore.bintray.io/tinycore:9.0-x86_64
/ $ grep -i pretty /etc/os-release
PRETTY_NAME="TinyCoreLinux 9.0"
```

A container build image is available, that feature tinycore with `compiletc` package:

``` console
$ sudo podman run -it boot2podman-docker-tinycore.bintray.io/tinycore-compiletc:9.0-x86_64
/ $ cc --version
cc (GCC) 7.2.0
```

## go

Another add-on image to it is also available, including the `go` compiler environment:

``` console
$ sudo podman run -it boot2podman-docker-tinycore.bintray.io/tinycore-go:1.10.4
/ $ go version
go version go1.10.4 linux/amd64
```

This sets up the needed variables (such as $PATH/$GOPATH), and `git` command:

``` console
/ $ go get github.com/golang/example/hello
/ $ hello
Hello, Go examples!
```

## Packages

Just run

```sh
sudo podman run -it boot2podman-docker-tinycore.bintray.io/tinycore:9.0-x86_64
```

To install tcz packages into the container and use them, run the `tce-load` command

```sh
tce-load -wic bash.tcz
```

or run the container with privilege mode like following

```sh
sudo podman run -it --privileged boot2podman-docker-tinycore.bintray.io/tinycore:9.0-x86_64
```

Once it starts with privilege mode, you can run the package manager like

```sh
tce-ab
```

## Upstream

These original packages are found under

- [http://tinycorelinux.net/9.x/](http://tinycorelinux.net/9.x/)

Container images have been adopted from

- [https://github.com/tatsushid/docker-tinycore](https://github.com/tatsushid/docker-tinycore)

## Source

See [https://github.com/boot2podman/boot2podman/tree/master/containers](https://github.com/boot2podman/boot2podman/tree/master/containers)

This includes all the build scripts to build the container images from `scratch`.
