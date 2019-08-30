# qemu-register

A simple way to register `qemu` usermode emulation binaries for your kernel.

[![Build Status](https://travis-ci.com/sfalexrog/qemu-register.svg?branch=master)](https://travis-ci.org/sfalexrog/qemu-register)

This repository is forked from [hypriot/qemu-register](https://github.com/hypriot/qemu-register) and is provided with minimal changes

## How this works

Starting with the Linux kernel 4.8, there's a mechanism in the kernel to load the interpreter specified in your `binfmt_misc` ahead of time (and make sure it stays in memory even if the interpreter file is deleted or moved). This is described in better detail in [this blog post by npmccallum](https://npmccallum.gitlab.io/post/foreign-architecture-docker/) and in the [kernel binfmt_misc docs](https://www.kernel.org/doc/Documentation/admin-guide/binfmt-misc.rst).

## Build Docker image

```bash
./build.sh
```

## Check Qemu binaries and versions

```bash
$ docker run --rm sfalexrog/qemu-register sh -c 'ls -al /qemu*'
-rwxr-xr-x    1 root     root       6192520 Apr 27 11:25 /qemu-aarch64
-rwxr-xr-x    1 root     root       5606984 Apr 27 11:25 /qemu-arm
-rwxr-xr-x    1 root     root       5987464 Apr 27 11:25 /qemu-ppc64le

$ docker run --rm hypriot/qemu-register /qemu-arm --version
qemu-arm version 4.0.0 (v4.0.0-dirty)
Copyright (c) 2003-2019 Fabrice Bellard and the QEMU Project developers

$ docker run --rm hypriot/qemu-register /qemu-aarch64 --version
qemu-aarch64 version 4.0.0 (v4.0.0-dirty)
Copyright (c) 2003-2019 Fabrice Bellard and the QEMU Project developers

$ docker run --rm hypriot/qemu-register /qemu-ppc64le --version
qemu-ppc64le version 4.0.0 (v4.0.0-dirty)
Copyright (c) 2003-2019 Fabrice Bellard and the QEMU Project developers
```

## Run the resulting Docker image to register the Qemu interpreters

```bash
docker run --rm --privileged hypriot/qemu-register
```

## Buy the authors a beer!

This FLOSS software is funded by donations only. Please support the original authors to maintain and further improve it!

<a href="https://liberapay.com/Hypriot/donate"><img alt="Donate using Liberapay" src="https://liberapay.com/assets/widgets/donate.svg"></a>
