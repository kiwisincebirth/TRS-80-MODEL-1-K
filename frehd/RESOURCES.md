# FreHD Resources and FAQ

## Resources

Some useful links from the author:
* The [authors main website](https://www.vecoven.com/trs80/trs80.html), historical information
* The [authors downloads](https://www.vecoven.com/trs80/trs80/download.html), which are a bit legacy
* The [authors GITHUB repo](https://www.vecoven.com/trs80/trs80.html), seems to have most upto date software

The GIT Hub Repo contains some important software locations
* HW/GAL - The coded deployed on GAL chip
* SW/TRS_HARD - The PIC microcontroller Software
* SW/FREHD_ROM - The software that build the FREHHD.ROM loader installed on SD Card
* SW/FREHD_ROM/PATCHES - Changes to TRS-80 Rom images, for autoboot
* SW/Z80/UTILS - The Z80 utility applications that run on TRS-80

And forked / related repositories
* [ontheslab/FreHDv1CPM](https://github.com/ontheslab/FreHDv1CPM), contains downloadable software releases.
* [maboytim/FreHDv1](https://github.com/maboytim/FreHDv1), contains alterations and improvements

Then there is Ian Mavrick's site, which has commercial product offerings, selling the FreHD. 
Important Links from Ian M's site:
* [FreHD Hard Drive Emulator](https://trs-80.com.au/trs80/emulator.htm)
* [Downloads](https://trs-80.com.au/trs80/downloads.htm) - Links may appear broken

Note: The download links on the above site are HTTP and need to be changed
to HTTPS (manually) as modern browsers will not download from HTTP. Copy the link, 
paste it into browser and change, make sure it says HTTPS

## Firmware Versions

The following FreHD firmware versions are known to exist

| Version | Description                                    | Where         |
|---------|------------------------------------------------|---------------|
| 2.13    | Is listed on Ian M's downloads Page            | Ian M         |
| 2.14    | Last version the author seemed involved with   | Ian M, Author |
| 2.15    | Seems to be distributed with purchased FreHD   | Purchase      |
| 2.16    | Was quickly superseded by 2.17                 | GitHub        |
| 2.17    | Latest (Sept 2024), with various fixes.        | Github        |

## SD Card Setup

Cards must be formatted on a PC in FAT32 only, and must have a volume name, 
leaving the name blank will result in a card which will not mount.

There are two things needed for operation, FREHD.ROM, and Hard Disk Images.

### FREHD.ROM

There seem to be a several of versions of `FREHD.ROM`, that offer different functionality.

| Version | Date     | Source                               | Supports  |
|---------|----------|--------------------------------------|-----------|
| 0E1Ah   | 2014 Mar | Original v2.14 from authors website  | LDOS ND80 |
| ? (*1)  | 2016 Feb | Provided by Ian Mav - on his website | All       |
| 1009h   | 2024 Aug | Github v2.17 distribution            | LDOS ND80 |
| 0999h   | 2024 Dec | Included with MultiDOS distribution  | All       |

The version provided by Ian M (*1) on his website has a different look and feel:
* "FreHD" Logo has a box around it instead of an underlined Logo
* All version info (firmware, bootloader, and ROM) has been removed.

The links for these downloads are covered in the rest of this document.
I would **recommend** the MultiDOS version as it is the latest, 
has compatability with all DOS's, and displays useful version information

The direct Link to download the Model 1 MultiDOS is - 
[md5101fh.zip](https://www.trs-80.com/cgi-bin/down-sw-model1.pl?md5101fh.zip)

### Hard Disk Images

The best primary location for downloads is Ian M's website.
you need to download the combined ZIP files that contain disk images, 
and includes FreHD.ROM.

There are 2 ZIP files for primary download
* [SD Card Model 1 - Floppy](https://trs-80.com.au/downloads/SDcardM1auto.zip) - 
* [Quinnerface - No Floppy](https://trs-80.com.au/downloads/Quinnterface.zip) - 

The downloads include LDOS 5.3.1, NEWDOS/80 2.5, DOSPLUS 3.5.
Multidos is not included in these images, it is downloadable separately.

While named quinnerface, i believe this includes disk images that don't support 
normal floppy drives.

## Operation

### LED's
* Green LED flashes once at startup to indicate that it has booted
* Green LED flashes when accessing the FreHD, includes any access e.g. reading time.
* Red led flashes when a card is inserted and no file system (FS) can be mounted
* Red LED is just a error or warning LED.
* RED LED ON, indicates that it is NOT safe to remove the SD card
* If both LEDs are solid ON, the emulator is in bootloader mode
 
## OS's

On a Model 1 there are several operating systems supported:
* DOSPLUS 3.5
* LDOS 5.3.1
* NEWDOS/80 2.5
* MULTIDOS 5.1

Overview of Dos's on the TRS-80
* [Model 1 Disk Operating Systems](http://cpmarchives.classiccmp.org/trs80/mirrors/kjsl/www.kjsl.com/trs80/model1info.html)

### DOSPLUS

[DOSPLUS Reference](https://www.trs-80.com/wordpress/reference/dosplus/)

The second partition `DIR :1` appears to have a few games preloaded

### LDOS

#### Disable Floppy Disks

If you want to use LDOS without an Expansion Interface (floppy disks), you may find it hangs.
There are a couple of extra setup steps. Immediately after loading LDOS, issue these commands
to disable floppy drives:

```
SYSTEM (DRIVE=6,DISABLE)
SYSTEM (DRIVE=7,DISABLE)
SYSTEM (SYSGEN)
```

#### Mount Floppy Disks

A LSDOS utility (works with LDOS5 and LSDOS6) which allows to mount one or more .dsk image,
directly from the SD card. It is written as an LSDOS driver, so you use it with

SYSTEM(DRIVE=x,DRIVER="DSK/DCT").

The driver will prompt you for the image name, then you can *read* from that image
(works great with DISKCOPY to make new boot disks, for example).
The dsk image is mounted read-only, there is no support for writes.
The usual emulated formats are supported : DMK, JV1 and JV3.

There is also a `DSK.CMD` file.

### NEWDOS/80

[NEWDOS/80 Reference](https://www.trs-80.com/wordpress/reference/newdos80/)

On systems without floppy disks the simplest way I have found to disable them is to use the system command

```
SYSTEM 0,AL=6
```

which set only 6 drives (assuming the first 6 are harddrives) as active excluding the latter floppy disks

### MultiDOS

[TRS-80 DOS – MultiDOS](https://www.trs-80.com/wordpress/reference/multidos/)

MultiDOS 5.1 was released in October 2023 by Vernon Hester, with a specific hard disk image for the FreHD.
A presentation was given at Tandy Assembly by Tim Halloran. 

Useful Links:
* [Using MULTIDOS: An Introduction for Today's TRS-80 Enthusiast](https://www.youtube.com/watch?v=3Ws1bQWp534) - Tandy Assembly 2023 Presentation
* [TRS-80 – Software Manuals – I-P](https://www.trs-80.com/wordpress/publications/manuals-software-2/) - Documentation - Search page for "MultiDOS"
* [TRS-80 DOS – MultiDOS](https://www.trs-80.com/wordpress/reference/multidos-4/) - Download - Search page for "FreHD"

Notes:
* A specific FreHD.ROM was included with the release which includes support for MultiDOS.
* The Documentation page contains original manuals, plus a FreHD specific guide.

## UTILITIES

The current version of these is 2.05a, whereas hard drive images generally have 2.03

The **latest versions** can be downloaded from the FreeHDv1CPM Github repository. Direct Link
* [ontheslab/FreHDv1CPM](https://github.com/ontheslab/FreHDv1CPM/releases/tag/v2.05a-alltools)

| Utility | Description                                                    |
|---------|----------------------------------------------------------------|
| VHDUTL  | management, real time clock, mount and unmount, create volumes |
| IMPORT2 | Move file to HD Volume from SD Card                            |
| EXPORT2 | Move file from HD Volume back to SD Card                       |
| DSK/CMD | LDOS / LSDOS Disk (Floppy) Image mounter                       |
| DSK/DCT | LDOS / LSDOS Disk (Floppy) Image mounter                       |
| FUPDATE | Firmware Update for the PIC microcontroller.                   |
| EUPDATE | EEPROM Update ??? unsure what this does ???                    |

This document (from Ian M's site) describes the use of some these utilities
* [FreHD Utilities](https://trs-80.com.au/trs80/FreHD%20Utilities.docx)


