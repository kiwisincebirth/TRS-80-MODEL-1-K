# FreHD Resources and FAQ

## Resources

Some useful links from the author:
* The [authors main website](https://www.vecoven.com/trs80/trs80.html), historical information
* The [authors downloads](https://www.vecoven.com/trs80/trs80/download.html), which are a bit legacy
* The [authors GITHUB repo](https://www.vecoven.com/trs80/trs80.html), 

The GIT Hub Repo contains some important software locations
* HW/GAL - The coded deployed on GAL chip
* SW/TRS_HARD - The PIC microcontroller Software
* SW/FREHD_ROM - The software that build the FREHHD.ROM loader installed on SD Card
* SW/FREHD_ROM/PATCHES - Chnages to TRS-80 Rom images, for autoboot
* SW/Z80/UTILS - The Z80 utility applications that run on TRS-80

Important Links from Ian M's site
* [FreHD Hard Drive Emulator](https://trs-80.com.au/trs80/emulator.htm)
* [Downloads](https://trs-80.com.au/trs80/downloads.htm) - Links may appear broken

Note: The download links on the above site are HTTP and need to be changed
to HTTPS (manually) as modern browsers will not download from HTTP. Copy the link, 
paste it into browser and change, make sure it says HTTPS

## Firmware Versions

| Version | Description                                                    |
|---------|----------------------------------------------------------------|
| 2.13    | Is still listed on on Ian M's downloads Page                   |
| 2.14    | The last version the author seemed actively involved with      |
| 2.15    | Seems to be the one currently distributed with purchased FreHD | 
| 2.17    | Latest On Github, contains some more recent fixes              |

## SD Card Setup

Cards must be formatted on a PC in FAT32 only.
Card must have a volume name, leaving the name blank will result in a card which will not mount.

### FREHD.ROM

There seem to be a couple of versions of this, the Header/banner appears differently 
Suggest use the download links below

### Downloading

If downloading from Ian's Site, I suggest you use the combined ZIP files 
that contain disk images, they seem to have a newer version.

There are 2 disk Images for primary download
* [SD Card Model 1 - Floppy](https://trs-80.com.au/downloads/SDcardM1auto.zip) - 
* [Quinerface - No Floppy](https://trs-80.com.au/downloads/Quinnterface.zip) - 

## Operation

### LED's
* Green LED flashes once at startup to indicate that it has booted
* Green LED flashes when accessing the FreHD, includes any access e.g. reading time.
* Red led flashes when a card is inserted and no file system (FS) can be mounted
* Red LED is just a error or warning LED.
* RED LED ON, indicates that it is NOT safe to remove the SD card
* If both LEDs are solid ON, the emulator is in bootloader mode
 
## OS's

On a Model 1 there appear to only be 2 OS 
* NEWDOS/80 2.5
* LDOS 5.3.1

### NEWDOS/80

### LDOS

If you want to use LDOS without an Expansion Interface (floppy disks), you may find it hangs.
There are a couple of extra setup steps. Immediately after loading LDOS, issue these commands:

```
SYSTEM (DRIVE=6,DISABLE)
SYSTEM (DRIVE=7,DISABLE)
SYSTEM (SYSGEN)
```

which disables floppy drives.

## UTILITIES

The current version of these is 2.05, whereas hard drive images generally have 2.03

| Utility  | Description                                                    |
|----------|----------------------------------------------------------------|
| IMPORT2  | Move file to HD Volume from SD Card                            |
| EXPORT2  | Move file from HD Volume back to SD Card                       |
| VHDUTL   | management, real time clock, mount and unmount, create volumes |
| FUPDATE  | Firmware Update for the PIC microcontroller.                   |
| EUPDATE  | EEPROM Update ?                                                |

This document describes the utilities
* [FreHD Utilities](https://trs-80.com.au/trs80/FreHD%20Utilities.docx)



