# Vampire boot

Vampire boot is a ready made HDF image, which can be installed in Amiga internal IDE port and configured to boot a partition on SD card installed in Apollo Vampire accelerator card. Currently Apollo Vampire accelerator card doesn't support autoboot partitions on SD card and that's there where Vampire boot comes to aid.

**Note: It's only been tested with Vampire 600 V2.**

## Description

Vampire boot consists of tools and scripts for Amiga to configure, mount and boot partitions on SD-card installed in Apollo Vampire accelerator card. It's based on SDMount from SAGA drivers with additional scripts and menu to simplify and automate configuration. This is done using GiggleDisk to build mountlist and patch mountlist to add filesystem handlers by examining DosType.

Startup for Vampire boot is done from CF/SD card installed in Amiga internal IDE port. It mounts devices listed in DEVS:mountlist and boots selected partition on Vampire SD-card.

![vampire_boot_1.png](screenshots/vampire_boot_1.png?raw=true)

## Requirements

Vampire boot requires an Amiga with Vampire card installed to work properly. It does work without Vampire card, but should only be used that way for testing purposes.

## Installation

Download latest release from https://github.com/henrikstengaard/vampire-boot/releases and write Vampire boot HDF file to CF/SD card. Install CF/SD card in A600 internal IDE port and power on Amiga.

## Setup

Vampire boot requires system files from Workbench 3.1 disk, which will be installed first time Vampire boot starts with a self install.
It automatically detects and use DF0:, DF1:, DF2: or DF3: containing required Workbench 3.1 disk.

When Workbench 3.1 system files are installed, Vampire boot will present a Configure Vampire Boot menu to build mountlist and select which partition to boot from SD card.

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

![vampire_boot_1.png](screenshots/vampire_boot_1.png?raw=true)

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

![vampire_boot_2.png](screenshots/vampire_boot_2.png?raw=true)

### Boot device menu

Boot Device menu lists devices from mountlist for selecting device to boot during startup of Vampire boot.

![vampire_boot_3.png](screenshots/vampire_boot_3.png?raw=true)

## Tutorial 1: Running Vampire boot self install in an emulator or on real Amiga

This tutorial describes step by step how to run Vampire boot self install in an emulator or on real Amiga.

Vampire boot self install can be run in following ways:

1. WinUAE: Start WinUAE using an A600/A1200 configuration with Vampire boot HDF added in CD & Hard drives.
2. Real Amiga: Write Vampire boot HDF to CF/SD card using Win32DiskImager and insert CF/SD card in Amiga internal IDE port.

**1. Start Vampire boot self install**.

Start Vampire boot self install in either an emulator or a real Amiga.

![run_self_install_1.png](screenshots/run_self_install_1.png?raw=true)

**2. Insert Workbench 3.1 disk**

Installation process will automatically detect and use DF0:, DF1:, DF2: or DF3: containing required Workbench 3.1 disk.

Insert required Workbench 3.1 disk in any floppy device and press enter to continue installation process.

![run_self_install_2.png](screenshots/run_self_install_2.png?raw=true)

![run_self_install_3.png](screenshots/run_self_install_3.png?raw=true)

**3. Workbench 3.1 installation**

Workbench 3.1 installation running and copying system files.

Press enter to continue installation process.

![run_self_install_4.png](screenshots/run_self_install_4.png?raw=true)

**4. Eject disk**

Eject Workbench 3.1 disk and press enter to continue installation process.

![run_self_install_5.png](screenshots/run_self_install_5.png?raw=true)

**5. Vampire boot installation complete and reboot**

Vampire boot installation is complete. 

Press enter to continue reboot.

![run_self_install_6.png](screenshots/run_self_install_6.png?raw=true)

**6. Vampire boot ready for use**

Vampire boot is now ready for use and can be configured.

![vampire_boot_1.png](screenshots/vampire_boot_1.png?raw=true)

## Tutorial 2: Configuring Vampire boot

This tutorial describes step by step how to configure Vampire boot in either an emulator or a real Amiga.

**1. Start Vampire boot**.

Start Vampire boot either in an emulator or a real Amiga.

First time startup will show Configure Vampire Boot menu.

![vampire_boot_1.png](screenshots/vampire_boot_1.png?raw=true)

**2. Build mountlist**.

Click "Build mountlist" to build mountlist and mount startup.

![vampire_boot_1.png](screenshots/vampire_boot_1.png?raw=true)

Build mountlist and mount startup is done.

Press enter to continue and it will return to main menu.

![vampire_boot_2.png](screenshots/vampire_boot_2.png?raw=true)

**3. Boot device**.

Click "Boot device" to select boot device.

![vampire_boot_1.png](screenshots/vampire_boot_1.png?raw=true)

For this example click "DH0:" to select it as boot device.

**Note: Devices listed depend on partitions detected on SD card in Vampire accelerator card.**

![vampire_boot_3.png](screenshots/vampire_boot_3.png?raw=true)

![vampire_boot_4.png](screenshots/vampire_boot_4.png?raw=true)

**4. Exit and reboot**.

Configuration of Vampire boot is complete.

Click "Exit" to exit Configure Vampire Boot and reboot.

Vampire boot will now mount partitions on SD card in Vampire accelerator card and boot selected boot device.

![vampire_boot_5.png](screenshots/vampire_boot_5.png?raw=true)