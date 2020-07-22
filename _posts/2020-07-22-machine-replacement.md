---
title: "Machine Replacement"
layout: post
author: afbjorklund
---

# Machine Replacement

If you are looking for a replacement for `podman-machine` or `docker-machine`,<br />
you can use Vagrant to provision a virtual machine with Fedora or Ubuntu.

Since both `podman` and `docker` are now available as standard distro packages,
installation is just a `yum` or an `apt` away (the deb package is called "docker.io").

## Manage as non-root user

If you install the normal package, you will have to use `sudo` to run it.
This becomes a problem, when trying to access the service from remote...

But it is possible to add a system group, to be used instead of `root`,
so that additional users can have socket access - without having to use sudo.

<https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user>

> Create the docker group.
>
> `$ sudo groupadd docker`
>
> Add your user to the docker group.
>
> `$ sudo usermod -aG docker $USER`

This also means that we can use a unix socket, instead of a tcp port:

`unix://[/path/to/socket]`

`tcp://[host]:[port][path]`

We use ssh to access this socket remotely, rather than a separate port.

### Security

Note that being part of this group allows running privileged containers:

> Warning: The docker group grants privileges equivalent to the root user.

It is also possible to run rootless containers, that is not the topic here.

We assume that the user is already part of the sudoers without a password.

## Vagrant with VirtualBox

Save to a `Vagrantfile`, and use `vagrant up` to boot the virtual machine.

### Podman (Fedora)

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "fedora/32-cloud-base"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum install -y podman

    groupadd -f -r podman

    #systemctl edit podman.socket
    mkdir -p /etc/systemd/system/podman.socket.d
    cat >/etc/systemd/system/podman.socket.d/override.conf <<EOF
[Socket]
SocketMode=0660
SocketUser=root
SocketGroup=podman
EOF
    systemctl daemon-reload
    echo "d /run/podman 0770 root podman" > /etc/tmpfiles.d/podman.conf
    systemd-tmpfiles --create

    systemctl enable podman.socket
    systemctl start podman.socket

    usermod -aG podman $SUDO_USER
  SHELL
end
```

### Docker (Ubuntu)

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    # focal64 bug: https://bugs.launchpad.net/cloud-images/+bug/1829625
    vb.customize [ "modifyvm", :id, "--uartmode1", "file", File::NULL ]
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update && apt-get install -y docker.io

    systemctl disable snapd.socket snapd.service
    systemctl stop snapd.socket snapd.service

    systemctl enable docker.socket docker.service
    systemctl start docker.socket docker.service

    usermod -aG docker $SUDO_USER
  SHELL
end
```

### Access

The virtual machine has been booted, and systemd has enabled the socket.

You can now use the `vagrant ssh` command, to access the virtual machine.

```shell
vagrant ssh -c "sudo podman version"
vagrant ssh -c "sudo podman info"
```

Have to use `sudo` here, or it would still try to run the rootless podman.

```shell
vagrant ssh -c "docker version"
vagrant ssh -c "docker info"
```

### Provider

It is also possible to use the libvirt/kvm provider when running on Linux.

But you probably have to use the "generic" images, from the Vagrant Cloud:

* <https://app.vagrantup.com/generic/boxes/fedora32>

* <https://app.vagrantup.com/generic/boxes/ubuntu2004>

Only the provider changes in the Vagrantfile, provisioning stays the same:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "generic/fedora32"

  config.vm.provider "libvirt" do |lv|
    lv.memory = "1024"
  end

  ...
```

## Configure client

Previously we would use podman varlink or the docker port 2376 to access,
but now both of them are using unix sockets over ssh connections instead...

Use `vagrant up` to start and `vagrant ssh-config` to see the configuration.
Then use variables from this ssh_config, to configure the ssh connection:

```text
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile $PWD/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

### Podman Remote

```shell
export CONTAINER_HOST=ssh://vagrant@127.0.0.1:2222/run/podman/podman.sock
export CONTAINER_SSHKEY=$PWD/.vagrant/machines/default/virtualbox/private_key
```

You currently **have** to supply the path of the unix socket, or it gets confused:

`ssh: rejected: connect failed (open failed)`

Note that podman uses CONTAINER_HOST and Containerfile, instead of "podman".

### Docker CLI

```shell
export DOCKER_HOST=ssh://vagrant@127.0.0.1:2222 # /var/run/docker.sock
ssh-add -k .vagrant/machines/default/virtualbox/private_key
```

When using docker it is **not** supported to supply the path of the unix socket:

`ssh host connection is not valid: extra path after the host`

The docker client doesn't support ssh identity, so the `ssh-agent` is used here.

## Links

Previous information:

* [Introducing Podman Machine]({% post_url 2018-12-04-introducing-podman-machine %})
* [Boot2Docker deprecated]({% post_url 2020-07-05-boot2docker-deprecated %})
