# TRS-80-MODEL-1-K

TRS-80 Model 1k - Hardware Replacement Main board - Evolution (Rev K)

## Introduction

This project is an upgraded / evolved TRS-80 Model 1 main board replacement. It was designed to provide a reliable, 
compact, and modern replacement, removing some limitations of the original 1970's product, 
while still remaining faithful to the original technology (i.e. no emulation) 

![MainboardFrontBuiltK1](/images/IMG_8736.jpeg)

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

### What is provided:
- All required materials and guides to order and assemble this project.
- A [FreHD board](/frehd/README.md) that can be connected directly to the mainboard, and installed internally. 
- A selection of [fonts files](/fonts/README.md) for use with this project.

## Features

The board started with the Japanese board as a base, because it is slightly upgraded over the US board 
with some minor improvements that carry over:
- The Video sync has been upgraded with improved stability, and 50Hz support
- The cassette input has minor improvements in the A/D design.

This means the Japanese Service manual has be used as a base for the basic schematic and component ID's as 
they are quite different to the US Model 1. Having said this the board itself has deviated
significantly so the provided schematics should be used.

The Japanese "specific" features have been removed to align this back to being a US Model 1. This includes the 
keyboard and Japanese Kana character set support.

This system is intended to be used (almost) exclusively with CMOS technology utilizing 74HCT (CMOS TTL compatible) parts.
Noting traditional 74LS components should work, however this has not been tested

### CPU

A double speed (3.56 Mhz) clock speedup mod has been applied. A jumper (J18) allows the clock to be slowed to normal. 
This could be by external switch, or any future circuit potentially under software control. See U1, U2 in schematic.
Note: If the cassette motor is turned on the speed will automatically be slowed.

The use of a modern CMOS Z-80 CPU is preferable

### System ROM

Uses a standard 27xxx EPROM (or 28256 EEPROM) rather than mask ROM. These are more readily available and easier to program. 
The two ROM's (Z42, Z43) have been replaced with a single 28 pin EPROM (U42) supporting 2x128 thru 2x512 chips. 
The board has jumpers to configure the ROM type, and/or 16kB page used for larger ROMS

An additional set of jumpers allows the ROM to provide an addition 1 or 2kBytes in the memory address 
above the ROM (0x3000 - 0x37FF), allowing a total of 12,13, or 14 kBytes of ROM. This can be useful for ROM extensions, 
commonly used on some Model 1 peripherals, or the Model 3.

### System RAM

The 4116 16kb DRAM has been replaced with a single static RAM chip (AS6C1008) U15 providing 48KB of RAM without the 
need for an external expansion interface or other add on card. Note this chip is 128 kBytes in size, but only 48kB 
is being used. No provision for RAM paging has been made.

If you intend to connect an expansion interface then the RAM in the interface will have to be disabled to prevent conflict.

### Character Generation

All character generation (both alpha characters and graphics) has been replaced with a single character set 
that includes all 256 characters defined in ROM (U37). Each character defines the full 6x12 pixel matrix that is 
generated. This approach is identical to the Gendon3 Model 1 font upgrade, and supports full lower case descenders.
The fonts used are compatible with Glens Stuff TRS-80 Model 1 Clone.

Each character requires 16 bytes (12 bytes used) per character, for a total of 4k bytes for the entire 256 character set.
Multiple character sets  can be defined (depending on ROM size), the character set chosen is configured by onboard dip switches.

A selection of [fonts files](/fonts/README.md) for use with this project. Normal font ROM's are not compatible.

### Video Output

Composite video output is via the original DIN plug, or an optional RCA connector, you can solder either onto the board. 
The RCA connector is provided to be compatible with a larger range of external monitors, potentially more reliable and 
less subject to noise.

### Internal Expansion:

The main board has an internal 40pin Header (J20) identical to and located just behind the main 40 pin expansion port. 
This is primarily designed for an internal expansion board which sits inside the case. 
The primary advantage being compactness. A optional second connector provides +5V in a four pin header (J21) for powering 
a internal expansion board.

See the [FreHD folder](/frehd/README.md) for a 40 pin FreHD that connects directly to this header.

Routing an external 40 pin ribbon cable to the connector is also possible, bypassing the 'unreliable' card edge connector.

Also provided for expansion are:
- Pin Header (J13) for internal audio amplifier, taken from cassette output
- Pin Header (J14) for internal reset signal, mirroring the external reset switch
- Pin Headers (J15,J16) are for internal 5V power for any other devices
- Pin Headers (J17) for internal (un-switched) +5V (both pins) power, for any devices requiring constant power

NOTE: The DRAM multiplexing signals CAS, and MUX are no longer generated, and have be removed on the main expansion connector.

A prototyping area is self explanatory, it has 12 chip supporting 14 or 16 pin power and locations for decoupling capacitors. 
This was included to add minor new features without the fragility of piggy back boards, or IC's

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

See the separate [Status and Future](/STATUS.md) which provides a mini update blog for this project

## Building

See the separate [Builders Guide](/BUILDING.md) for complete technical documentation

## Credits

- The Board Folk Ver 1.1 Japanese board without which this project would not be possible.
    - https://github.com/Board-Folk/TRS80IJP
- Glens stuff TRS-80 Model 1 clone, of which some inspiration was taken.
    - https://www.glensstuff.com/trs80/trs80.htm
- VCF Forums for some help and guidance
    - https://forum.vcfed.org/index.php?threads/trs-80-model-1-board-design.1251905/
- The Tandy Discord Channel for help and support
