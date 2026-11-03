# Installation

> **Experimental and incomplete:** this repository does not currently provide a bootable image, a tested installer, or verified device-flashing instructions. Installing an incompatible kernel or writing to the wrong partition can make the tablet unbootable or erase data. Do not flash artifacts from this project unless you have verified the exact device model, partition layout, and recovery procedure.

## Before attempting installation

- Confirm the tablet is the Lenovo Tab TB311FU; do not assume instructions apply to other Lenovo models or regional variants.
- Back up all important data and make sure you can restore the stock firmware using a known-good recovery process.
- Ensure the bootloader state, partition layout, and required boot image format are documented for your exact device.
- Use only kernel, modules, firmware, and root filesystem artifacts built for the same source revision and configuration.

## Current status

There is no installation image or installation script in this repository yet. Boot image packaging, partition mapping, first-boot setup, and rollback/recovery steps have not been documented or validated. The upstream project is a useful hardware reference, but it targets a different Linux distribution and its installation guidance must not be assumed to apply to this Debian port:

- [Upstream project](https://github.com/soumarcelino/linux-lenovo-tb311fu)
- [Upstream installation guide](https://github.com/soumarcelino/linux-lenovo-tb311fu/blob/main/docs/install.md)

## When a Debian image is available

The project should publish device-specific instructions alongside each tested image, including its checksum, kernel and toolchain revisions, required firmware, bootloader requirements, exact installation procedure, first-boot steps, and recovery instructions. Until that is available, treat the port as development work and do not write unverified artifacts to the tablet.
