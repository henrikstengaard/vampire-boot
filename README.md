# Vampire boot

Vampire boot is a ready made HDF image, which can be installed in Amiga internal IDE port and configured to boot a partition on SD-card installed in Apollo Vampire accelerator card. Currently Apollo Vampire accelerator card doesn't support autoboot partitions on SD-card and that's there where Vampire boot comes to aid.

**Note: It's only been tested with Vampire 600 V2.**

## Description

Vampire boot consists of tools and scripts for Amiga to configure, mount and boot partitions on SD-card installed in Apollo Vampire accelerator card. It's based on SDMount from SAGA drivers with additional scripts and menu to simplify and automate configuration. This is done using GiggleDisk to build mountlist and patch mountlist to add filesystem handlers by examining DosType.

Startup for Vampire boot is done from CF/SD-card installed in Amiga internal IDE port. It mounts devices listed in DEVS:mountlist and boots selected partition on Vampire SD-card.

## Requirements

Vampire boot requires an Amiga with Vampire card installed to work properly. It does work without Vampire card, but should only be used that way for testing purposes.

## Installation

Download latest release from https://github.com/henrikstengaard/vampire-boot/releases and write Vampire boot HDF file to CF/SD-card. Install CF/SD-card in A600 internal IDE port and power on Amiga.

## Setup

Vampire boot requires system files from Workbench 3.1 disk, which will be installed first time Vampire boot starts.
It automatically detects and use DF0:, DF1:, DF2: or DF3: containing required Workbench 3.1 disk.

When Workbench 3.1 system files are installed, Vampire boot will present a Configure Vampire Boot menu to build mountlist and select which partition to boot from SD-card.

## Startup sequence

Vampire boot startup sequence does following during boot:

1. Show Configure Vampire Boot menu if:
    1. V key is pressed.
    2. Boot device file "SYS:Prefs/Env-Archive/BootDevice" doesn't exist.
    3. Boot device is empty or set to VB0:.
    4. Mount startup file "S:Mount-Startup" doesn't exist.
    5. Mount startup file "S:Mount-Startup" contains VB0: device.
2. Execute S:Mount-Startup
3. Add assigns for boot device and executes it's startup-sequence.

## Configure Vampire Boot menu

Configure Vampire Boot menu has following options:

- Build mountlist: Build mountlist and mount startup.
- Boot device: Enters boot device menu.
- CLI: Starts CLI for tweaking purposes.
- Exit: Exit Configure Vampire Boot and reboots.

Screenshot of Configure Vampire Boot menu.

![Configure Vampire Boot menu](screenshots/vampire-boot1.png?raw=true)

### Build mountlist

Build mountlist uses GiggleDisk to build mountlist using sagasd.device. It uses VampireTool to detect Vampire card. 
If Vampire card is installed it uses sagasd.device, otherwise it uses scsi.device as a fallback.

Mountlist build by GiggleDisk doesn't have filesystem handlers defined and these are required to mount devices.
Patch mountlist updates mountlist with filesystem handlers by examining DosType. It currently supports following DosTypes:

| DosType | Filesystem | Handler |
| --- | --- | --- |
| 0x444f5303 | FastFileSystem | L:FastFileSystem |
| 0x50465303 | PFS3 | L:pfs_aio-handler |
| 0x46415401 | FAT32 | L:fat95 |

**Note: It's only been tested with PFS3 filesystems.**

![Build mountlist](screenshots/vampire-boot2.png?raw=true)

### Boot device menu

Boot Device menu lists devices from mountlist for selecting device to boot during startup of Vampire boot.

![Select Boot Device menu](screenshots/vampire-boot3.png?raw=true)