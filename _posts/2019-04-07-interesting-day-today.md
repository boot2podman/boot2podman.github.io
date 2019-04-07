---
layout: post
title:  "Interesting Day Today"
author: afbjorklund
---

# Interesting Day Today

Spent the day in Göteborg at the [FOSS North Community Day](https://foss-north.se/2019/community-day.html), and it was interesting.

First spent some time with BSD people and then GNU people, getting two different sides.

Thanks to B3 and Kuro for hosting, and to **all** working on Free and Open Source Software!

The rest of this post is related to containers (in general) and to podman (in particular)...

## FreeBSD

<https://wiki.freebsd.org/DevSummit/201904>

While it would be possible to use `runc` and containers in Jails, it's **not** out-of-the-box.

There were efforts to port Docker, but they seem halted: <https://wiki.freebsd.org/Docker>

See <https://github.com/kvasdopil/docker/blob/freebsd-compat/FREEBSD-PORTING.md>

FreeBSD runc: <https://github.com/clovertrail/runc/tree/1501-SupportOnFreeBSD> (OCI)

So it seems unlikely to have full support [^1] for running Linux containers, any time soon...

[^1]: like it is with "Linux branded Zones" on [SmartOS](https://www.joyent.com/smartos), for instance...

But I don't see any problems of making `podman-machine` [^2] available in the meantime.

[^2]: FreeBSD is running [docker-machine](https://svnweb.freebsd.org/ports/head/sysutils/docker-machine/) today, for [docker](https://svnweb.freebsd.org/ports/head/sysutils/docker/) support...

## Debian

<https://wiki.debian.org/BSP/2019/04/se/Gothenburg>

Debian packaging of Docker is interesting, they have broken `vendor` up into packages.

<https://www.collabora.com/news-and-blog/blog/2018/07/04/docker-io-debian-package-back-to-life/>

This is probably _the right thing to do_, but it also means trouble for a podman `.deb`.

Basically there needs to be a separate build dependency, for _each_ library under vendor/*.

Some of them are internal and can be combined, but they all need to be gone through [^3].

[^3]: currently there are a 100+ such dependencies, even more in c/image and c/storage.

It is still possible to do like the Ubuntu PPA (or various RPM), and just do a static build [^4].

[^4]: i.e. all the dependencies are packaged up, but the Go libraries just use vendoring.

But is unlikely that it will go into Debian, <https://github.com/containers/libpod/issues/1742>

## Night

Day ended with a social event at the [Steampunk Bar](https://steampunkbar.se/), before [FOSS North](https://foss-north.se/) tomorrow.

Most likely there will be more discussion on containers to come (Lightning Talk on Tue).

----