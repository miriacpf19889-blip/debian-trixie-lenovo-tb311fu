# Build guide

This experimental project does not yet build a complete Debian image. The script below builds the upstream TB311FU Android Common kernel only; rootfs creation, boot image packaging, and installation are not automated here.

## 1. Install build tools

On a Debian 13 (Trixie) x86-64 host:

```sh
sudo apt update
sudo apt install -y git make python3 bc bison flex libssl-dev libelf-dev dwarves \
  gcc-aarch64-linux-gnu binutils-aarch64-linux-gnu
```

Allow plenty of free disk space for the kernel source and build output. The Android Clang r510928 toolchain is also required; obtain it using the upstream project's toolchain instructions. The script does not download the toolchain automatically.

## 2. Clone this project

```sh
git clone https://github.com/miriacpf19889-blip/debian-trixie-lenovo-tb311fu.git
cd debian-trixie-lenovo-tb311fu
```

## 3. Set the toolchain path

Set `CLANG_BIN` to the directory containing the toolchain's `clang` executable. For example, if Clang is installed at `$HOME/toolchains/clang-r510928/bin/clang`:

```sh
export CLANG_BIN="$HOME/toolchains/clang-r510928/bin"
```

## 4. Build the kernel

```sh
chmod +x scripts/build-kernel
JOBS="$(nproc)" ./scripts/build-kernel
```

The script clones the upstream device configuration and Android Common kernel into `build/sources/`, checks out the pinned revisions, applies the upstream host-OpenSSL compatibility patch, and builds the arm64 `Image` and kernel modules. The first run downloads a large kernel source tree and can take a while.

Expected kernel image:

```text
build/kernel/arch/arm64/boot/Image
```

To use existing source/output directories, set `UPSTREAM_DIR`, `KERNEL_SRC`, `KERNEL_OUT`, or `BUILD_DIR` before running the script. `CLANG_BIN` is required. `JOBS` controls parallel build jobs.

## What is not built yet

This script does not create a Debian Trixie root filesystem or a flashable/bootable device image. It also does not install modules into a rootfs, package firmware, or flash the tablet. Those steps need device-specific packaging and verified installation instructions before they can safely be automated.

## References

- [Upstream build guide](https://github.com/soumarcelino/linux-lenovo-tb311fu/blob/main/docs/build.md)
- [Upstream kernel source manifest](https://github.com/soumarcelino/linux-lenovo-tb311fu/blob/main/kernel/source.json)
