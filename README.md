# Vampire boot

Vampire boot is a setup tools and scripts for Amiga to configure, mount and boot partitions on SD-card installed in Apollo Vampire accelerator card. This is required for booting partitions on Vampire SD-card as it currently doesn't automatically boot partitions on SD-card.

Startup for Vampire boot is done from CF/SD-card installed in A600 internal IDE port. It mounts devices listed in DEVS:mountlist and boots selected partition on Vampire SD-card.

Vampire boot is based on SDMount from SAGA drivers with additional scripts and menu to simplify and automate configuration. This is done using GiggleDisk to build mountlist and patch mountlist to add filesystems by examining DosType.

## Requirements

Vampire boot requires an Amiga with Vampire card installed to work properly. It does work without Vampire card, but should only be used that way for testing purposes.

## Installation

Download latest release from https://github.com/henrikstengaard/vampire-boot/releases and write Vampire boot HDF file to CF/SD-card. Install CF/SD-card in A600 internal IDE port and power on Amiga.

## Setup

Vampire boot requires system files from Workbench 3.1 disk, which will be installed first time Vampire boot starts.
It automatically detects and use DF0:, DF1:, DF2: or DF3: containing required Workbench 3.1 disk.

When Workbench 3.1 system files are installed, Vampire boot will present a Configure Vampire Boot menu to build mountlist and select which partition to boot from SD-card.

## Startup sequence

TODO

## Configure Vampire Boot menu

Configure Vampire Boot menu has following options:

- Boot device: Enters select boot device menu.
- Build mountlist: Build mountlist, mount startup and reboots.
- CLI: Starts CLI for tweaking purposes.
- Exit: Exit Configure setup.

Screenshot of Configure Vampire Boot menu.

![Configure Vampire Boot menu](screenshots/vampire-boot1.png?raw=true)

## Select Boot Device menu

Select Boot Device menu lists devices from mountlist to select device to boot during startup of Vampire boot.

![Select Boot Device menu](screenshots/vampire-boot2.png?raw=true)