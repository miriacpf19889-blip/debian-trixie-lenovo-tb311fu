# Build

This repository is an experimental Debian 13 (Trixie) port for the Lenovo Tab TB311FU. The build pipeline is not yet implemented in this repository: it currently has no kernel configuration, build scripts, Debian rootfs recipe, or image packaging. Do not treat the commands below as a complete device-image build.

## Host prerequisites

Use a Debian 13 or compatible Linux x86-64 build host with:

- Git, `make`, Python 3, `bc`, `bison`, `flex`, `libssl-dev`, `libelf-dev`, and ` dwarves` (package name `dwarves`).
- An AArch64 cross compiler (for example, `gcc-aarch64-linux-gnu`).
- The Android Clang toolchain required by the upstream kernel project.
- `debootstrap` for creating a Debian Trixie arm64 root filesystem.
- Several tens of gigabytes of free disk space for source trees, build outputs, and the root filesystem.

Some packages may have different names on non-Debian hosts.

## Kernel and toolchain

The upstream TB311FU project documents Android Common kernel `android15-6.6.142_r00` at commit `1782065b5f3dad41d3785247e50820553c3473e6` and Android Clang `r510928`. Check the upstream build documentation before building, since its source and build requirements may change:

- [Upstream build guide](https://github.com/soumarcelino/linux-lenovo-tb311fu/blob/main/docs/build.md)
- [Upstream kernel source manifest](https://github.com/soumarcelino/linux-lenovo-tb311fu/blob/main/kernel/source.json)

The upstream build scripts expect to run from a checkout of that project, which contains device-specific kernel configuration and scripts. They are not included in this Debian repository yet. Do not run those commands from this repository and expect them to work.

## Debian root filesystem

The intended root filesystem is Debian Trixie for `arm64`. A future build script should bootstrap it with `debootstrap`, configure the target account and device adaptation, then install the matching kernel modules and firmware. Rootfs creation requires elevated privileges; keep it in a dedicated build directory and never point a bootstrap or cleanup command at a mounted host filesystem.

No rootfs bootstrap script or package list is currently provided here. Until those are added, rootfs creation and integration remain manual and unverified.

## Expected build outputs

A complete build should produce separately identifiable kernel, modules, and Debian rootfs artifacts under a build/output directory. This repository does not yet produce those artifacts. Record source revisions and toolchain versions alongside future release images so builds can be reproduced.
