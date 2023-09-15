# Build Hybrid Image

## Description

Given an existing Roadrunner-based disk image, this script builds a
new hybrid version with REVO's bootloader and devicetree. The kernel
is converted from zImage to uImage format, as required by REVO's
bootloader. The original disk image is unmodified.

A hybrid image can be built with the scripts in the repository
[build-hybrid-image](https://github.com/revolution-robotics/build-hybrid-image).
Instructions for installing and running it follow.

## Installation Prerequisites

The **build-hybrid-image** scripts depends on the following
packages/utilities:

- [bmap-tools](https://github.com/intel/bmap-tools)
- [buildah](https://github.com/containers/buildah)
- [file](https://github.com/file/file)
- [gawk](https://savannah.gnu.org/git/?group=gawk)
- [mount.image](https://github.com/revolution-robotics/mount.image)
- [parted](https://git.savannah.gnu.org/gitweb/?p=parted.git;a=summary)
- [podman](https://github.com/containers/podman)
- [uboot-tools](https://source.denx.de/u-boot/u-boot)
- [util-linux](https://github.com/util-linux/util-linux)

With the exception of **mount.image**, these can be installed by name,
e.g., on Fedora:

```bash
sudo dnf install -y bmap-tools buildah gawk parted podman uboot-tools util-linux
```

or on Debian/Ubuntu:

```bash
sudo apt install -y bmap-tools buildah gawk parted podman u-boot-tools util-linux
```

The **mount.image** script can be installed per the instructions on
its web page (see link above).

## Installation

After installing the prerequisites above, run:

```bash
git clone https://github.com/revolution-robotics/build-hybrid-image
cd ./build-hybrid-image
```

Edit the file *./build-hybrid-image.conf*, then run:

```
./build-hybrid-image
```

## Build Process

The
