# Build Hybrid Image

- [Description](#description)
- [Installation Prerequisites](#installation-prerequisites)
- [Installation and Build](#installation-and-build)
- [Inspecting/Modifying Hybrid Image](#inspectingmodifying-hybrid-image)
- [Inspecting Build System](#inspecting-build-system)

## Description

Given an existing Roadrunner-based disk image, the script
`build-hybrid-image` builds a new hybrid image with REVO's
bootloader and devicetree. The kernel is converted from zImage to
uImage format, as required by REVO's bootloader. The original disk
image is unmodified.

Additional scripts for inspecting the container build environment and
hybrid image are available in the repository
[build-hybrid-image](https://github.com/revolution-robotics/build-hybrid-image).
These scripts have been tested on Fedora (M1) and Ubuntu (x86_64)
systems. Instructions for installing and running them follow.

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
- [qemu-user-static](https://github.com/multiarch/qemu-user-static)
- [uboot-tools](https://source.denx.de/u-boot/u-boot)
- [util-linux](https://github.com/util-linux/util-linux)

With the exception of **mount.image**, these can be installed by name,
e.g., on Fedora:

```bash
sudo dnf install -y bmap-tools buildah gawk parted podman \
    qemu-user-static-arm uboot-tools util-linux
```

or on Debian/Ubuntu:

```bash
sudo apt install -y binfmt-support bmap-tools buildah gawk parted \
    podman qemu-user-static u-boot-tools util-linux
systemctl enable --now binfmt-support
```

The **mount.image** script can be installed per the instructions on
its web page (see link above).

## Installation and Build

After installing the prerequisites above, run:

```bash
git clone https://github.com/revolution-robotics/build-hybrid-image
cd ./build-hybrid-image
```

Edit the file *./build-hybrid-image.conf*, then run:

```bash
./build-hybrid-image
```

The hybrid image is saved to the path indicated in
*build-hybrid-image.conf*.

## Inspecting/Modifying Hybrid Image

The hybrid image can be mounted and inspected with the `mount.image`
command, e.g.:

```bash
mount.image /path/to/hybrid.wic.gz
```

Changes to the mounted file systems are saved back to the image when the
image is unmounted via:

```
umount.image /path/to/hybrid.wic.gz
```

## Inspecting Build System

The container used to build the REVO components can be entered
interactively with:

```bash
./run-roadrunner-container
```

At the Debian prompt, change to the root of the build system:

```bash
cd /root/roadrunner-debian
```

From there, the bootloader sources are in *src/uboot* and the kernel
sources in *src/kernel*.
