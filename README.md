# TRS-80-MODEL-1-K

TRS-80 Model 1k - Hardware Replacement Main board - Evolution (Rev K)

## Introduction

This project is an upgraded / evolved TRS-80 Model 1 main board replacement. It was designed to provide a reliable, 
compact, and modern replacement, removing some limitations of the original 1970's product, 
while still remaining faithful to the original technology (i.e. no emulation) 

![MainboardFront](/pcb/TRS-80-MP-FrontV2.png)

### What this is:
- Drop in (mostly) replacement main board for existing TRS-80 Model 1
- Modernised using larger density (memory) components to reduce component count
- Onboard some common features, that required a piggyback board's or piggyback IC's
- Provides some level of additional internal expansion, or ability to evolve the board itself.
- Remains faithful to the use of traditional thru-hole parts, and discrete logic IC's

### What this isn't:
- Is not compatible with 32Kb external RAM expansion, external RAM will need to be disabled
- Is not compatible with Model 1 unregulated power supply, requires regulated 5V power
- Is not a faithful recreation of the original Model 1, other projects exist for this.

## Features

The board started with the Japanese board as a base, because it is slightly upgraded over the US board with some notable 
minor improvements. This means the Japanese Service manual has be used as a base for the basic schematic and component ID's as 
they are quite different from the US Model 1.

The Japanese "specific" features have been removed to align this back to being a US Model 1. This includes the 
keyboard and Japanese Kana character set support.

This system is intended to be used (almost) exclusively with CMOS technology utilizing 74HCT (CMOS TTL compatible) parts.
Noting traditional 74LS components should work, however this has not been tested

### CPU

A selectable 2/3 clock speedup (3.5Mhz/5.3Mhz) mod has been made. A jumper (J18) allows the clock to be slowed to normal. 
This could be by external switch, or any future circuit potentially under software control.
Note: If the cassette motor is turned on the speed will automatically be slowed.

A pin Header next to CPU exposes /RD, /WR, and /M1, the essential signals used for Sigrok Z80 protocol decoding,
that are not exposed on the main expansion interface.
Other signals such as address and data lines can be obtained from expansion IO header (J20)

The Reset Switch can now be changed from a soft NMI Reset to a hard CPU Reset. Also, an onboard hard
reset is provided via pushbutton, for full reset during diagnostics

The use of a modern CMOS Z-80 CPU is preferable

### System ROM

Uses a standard 27xxx EPROM (or 28256 EEPROM) rather than mask ROM. These are more readily available and easier to program. 
The two ROM's (Z42, Z43) have been replaced with a single 28 pin EPROM (U42) supporting 2x128 thru 2x512 chips. 
The board has jumpers to configure the ROM type, and/or 16kB page used for larger ROMS.

An additional set of jumpers allows either ROM (or RAM) to be mapped in the memory address 
above the normal ROM (0x3000 - 0x37FF). This can be useful for custom ROM extensions, 
commonly used on some Model 1 peripherals, or RAM for any purpose

### System RAM

The 4116 16kb DRAM has been replaced with a single static RAM chip (AS6C1008) U15 providing 48KB of RAM without the 
need for an external expansion interface or other add on card. Note this chip is 128 kBytes in size, but only 48kB 
is being used. No provision for RAM paging has been made.

If you intend to connect an expansion interface then the RAM in the interface will have to be disabled to prevent conflict.

### Video RAM (V2)

One of the bigger issues with model 1 design was use of shared video ram with very primitive contention resolution.
The Model 1 video subsystem takes second priority to CPU, causing artefacts (snow) when CPU accesses video RAM during visible period.
The Model 3 somewhat improved this by asking CPU to wait for next blank interval, giving priority to video system.

Dual Port SRAM
- The chip itself has 2 channels/ports, mirroring all address data control lines as if a standalone chip. This accounts for the chips high 48 pin count
- Contention still exists but this is at byte level, Ie when both ports try to access the same address in RAM
- This significantly reduces the chance of contention when CPU accesses vram from about 33% (time when not blanking), to about  .033% a factor of 1024
- When contention occurs the second request (CPU or video side) receive a Busy signal, this as handled on the CPU side big signaling a WAIT. On the video side the existing logic is used, displaying artifacts.
- Chip count and complexity is reduced by removing address multiplexes, and data buffer to main data bus. From 6 (including 2 Ram chips) to single RAM large chip

### Character Generation

All character generation (both alpha characters and graphics) has been replaced with a single character set 
that includes all 256 characters defined in ROM (U37). Each character defines the full 6x12 pixel matrix that is 
generated, and requires 16 bytes (only 12 are used) per character, for a total of 4k bytes for the entire character set. 

Multiple character sets  can be defined (depending on ROM size), the character set chosen is configured by DIP Switches.
Also Port FF Bit 7 can be used to control the LSB of the character set selection 

Since characters sets can control all lines of the raster true lower case descender's can be defined i.e. Gendon3.
The fonts are compatible with Glens Stuff TRS-80 Model 1 Clone. Normal font ROM's are not compatible.

### Video Output

A modern video sync generation circuit exists which allows the H and V positions to be adjusted

Composite video output is via standard a RCA connector or the original DIN plug, you can solder either onto the board. 
The RCA connector is provided to be compatible with a larger range of external monitors, potentially more reliable and 
less subject to noise.

If using the DIN socket better support has been added to allow the use of RGBtoHDMI, by passing the HDRV signal to 
pin 3 of the DIN socket. This is enabled by bridging jumper JP15. See below for further details.

https://github.com/hoglet67/RGBtoHDMI/wiki/Cables#trs80-model-1-mono--video-genie

For tear free video output Tim Halloran's no chip VBLANK modification is provided. See following for details:

https://github.com/hallorant/bigmit/blob/master/ta19demo/README.md

### Sound Output (V2)

Sockets (U4 and U5) provide a location to install a small audio amplifier module, 
based on the LTK5128, or XPT8871 chipset. 2 headers are provided for 2 distinct pinout configurations.
A volume control is provided (RV2), with a speaker needing to be attached to (J8) 
If supported the amplifier will be muted when the cassette interface is active. 

### Joystick Port (V2)

An Alpha Joystick port (5 bit) on Ports 00h-0Fh. At this time 4 bit mode is not supported.

http://www.trs-80.org/alpha-joystick/

### Internal Expansion:

The main board has an internal 40pin Header (J20) identical to and located just behind the main 40 pin expansion port. 
This is primarily designed for an internal expansion board which sits inside the case. 
The primary advantage being compactness. A optional second connector provides +5V in a four pin header (J21) for powering 
a internal expansion board.
A few additional mounting holds have been provided to support an addon board

Routing an external 40 pin ribbon cable to the connector is also possible, bypassing the 'unreliable' card edge connector.

Also provided for expansion are:
- Pin Header (J14) for internal reset signal, mirroring the external reset switch, SW11 also provides PB switch
- Pin Headers (J15,J16) are for internal 5V power for any other devices
- Pin Headers (J17) for internal (un-switched) +5V (both pins) power, for any devices requiring constant power

NOTE: The DRAM multiplexing signals CAS, and MUX are no longer generated, and have be removed on the main expansion connector.
These two expansion pins can be re-used for any future purpose, they are exposed as solder pads on the PCB 

A prototyping area is self-explanatory, it has 11 chip supporting 14 or 16 pin power and locations for decoupling capacitors. 
This was included to add minor new features without the fragility of piggyback boards, or IC's

### Power

Replacing the RAM means the computer does not requires 12V and -5V power, only 5V is required. 
This has driven the transformation of the power system for the computer by moving the power regulation off the PCB itself, 
and instead requires a external 5V DC regulated power supply. The external TRS-80 power brick is no longer supported. 
Power connection is by the of a standard barrel jack replacing the DIN connector.

This leaves substantial PCB real-estate, which is available for future use and evolution of this board

The Power (and Reset) buttons have been superseded with more available standardized components. 
The original component footprints have still been left so can still install the original parts.

### Additionally

Additional changes have been made too numerous to mention please see [Changelog](/CHANGELOG.md) for details

## Status / Future

See the separate [Status and Future](/STATUS.md) 

## Building

See the separate [Builders Guide](/BUILDING.md) for complete technical documentation

## Credits

- The Board Folk Ver 1.1 Japanese board without which this project would not be possible.
    - https://github.com/Board-Folk/TRS80IJP
- Glens stuff TRS-80 Model 1 clone, of which some inspiration was taken.
    - https://www.glensstuff.com/trs80/trs80.htm
- VCF Forums for some help and guidence
    - https://forum.vcfed.org/index.php?threads/trs-80-model-1-board-design.1251905/
