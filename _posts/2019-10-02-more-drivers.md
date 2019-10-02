---
layout: post
title:  "More Drivers"
author: afbjorklund
---

# More Drivers

## Current Drivers

Currently podman-machine ships with the following drivers:

- `virtualbox` (default)
- `qemu` (kvm/hax/hvf)
- `generic` (ssh)

These are built-in, and don't require any external programs...

## Future Drivers

Not everyone likes VirtualBox or QEMU, so add more drivers:

- `libvirt` (linux)
- `hyperv` (windows)
- `xhyve` (darwin)

With the plugin functionality, they can be added externally.

## Difference

Mostly the podman-machine drivers are the _same_ as the ones<br>
for docker-machine, except for the url and the swarm support.

```diff
@@ -22,5 +22,2 @@
 	StorePath      string
-	SwarmMaster    bool
-	SwarmHost      string
-	SwarmDiscovery string
 }
@@ -79,9 +76,2 @@
 }
-
-// SetSwarmConfigFromFlags configures the driver for swarm
-func (d *BaseDriver) SetSwarmConfigFromFlags(flags DriverOptions) {
-	d.SwarmMaster = flags.Bool("swarm-master")
-	d.SwarmHost = flags.String("swarm-host")
-	d.SwarmDiscovery = flags.String("swarm-discovery")
-}
```

So it should be rather straight-forward to fork them for podman.<br>
Go makes it easy to cross-compile, use containers for the rest...

- <https://github.com/boot2podman/podman-machine-driver-libvirt>
- <https://github.com/boot2podman/podman-machine-driver-hyperv>
- <https://github.com/boot2podman/podman-machine-driver-xhyve>
