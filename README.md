# Vampire Boot

Vampire boot is a setup tools and scripts for Amiga to configure, mount and boot partitions on SD-card installed in Apollo Vampire accelerator card. This is required for booting partitions on Vampire SD-card as it currently doesn't automatically boot partitions on SD-card.

Startup for Vampire boot is done from CF/SD-card installed in A600 internal IDE port. It mounts devices listed in DEVS:mountlist and boots selected partition on Vampire SD-card.

At first time startup, Vampire boot will present a configure vampire boot menu to build mountlist and select which partition to boot from SD-card.

## Requirements

Vampire boot requires an Amiga with Vampire card installed to work properly. It does work without Vampire card, but should only be used that way for testing purposes.

## Installation

Download latest release from https://github.com/henrikstengaard/vampire-boot/releases and write Vampire boot HDF file to CF/SD-card. Install CF/SD-card in A600 internal IDE port and power on Amiga.

## Startup sequence

TODO

## Configure vampire boot menu

TODO