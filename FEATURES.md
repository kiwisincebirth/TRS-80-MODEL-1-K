# Features

## Base Features

The board started with the Japanese board as a base, because it is slightly upgraded over the US board
with some minor improvements that carry over:
- The Video sync has been upgraded with improved stability, and 50Hz support
- The cassette input has minor improvements in the A/D design.
- The video RAM was upgrade to full 8 bits using 2 x 2114 SRAM Chips

The Japanese "specific" features have been removed to align this back to being a US Model 1. This includes the
keyboard and Japanese Kana character set support.

This system is intended to be used (almost) exclusively with CMOS technology utilizing 74HCT (CMOS TTL compatible) parts.
Noting traditional 74LS components should work, however this has not been tested

### CPU

A double speed (3.56 Mhz) clock speedup mod has been applied. A jumper (J18) allows the clock to be slowed to normal.
This could be by external switch, or any future circuit potentially under software control.
Note: If the cassette motor is turned on the speed will automatically be slowed.

### System ROM

Uses a standard 27xxx EPROM (or 28256 EEPROM) rather than mask ROM. These are more readily available and easier to program.
The two ROM's (Z42, Z43) have been replaced with a single 28 pin EPROM (U42) supporting 2x128 thru 2x512 chips.
The board has jumpers to configure the ROM type, and/or 16kB page used for larger ROMS

An additional set of jumpers allows the ROM to provide an addition 1 or 2kBytes in the memory address
above the ROM (0x3000 - 0x37FF), allowing a total of 12,13, or 14 kBytes of ROM. This can be useful for ROM extensions,
commonly used on some Model 1 peripherals, or the Model 3.

### System RAM

The 4116 16kb DRAM has been replaced with a single static RAM chip (AS6C1008) providing 48KB of RAM without the
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

NOTE: The DRAM multiplexing signals CAS, and MUX are no longer generated, and have be removed on the main expansion connector.

A prototyping area is provided, it supports 14 or 16 pin power and locations for decoupling capacitors.
This was included to add minor new features without the fragility of piggy back boards, or IC's

### Power

Replacing the DRAM means the computer does not require -5V or 12V power, only 5V is required.
This has driven the transformation of the power system for the computer by moving the power regulation off the PCB itself,
and instead requires a external 5V DC regulated power supply. The external TRS-80 power brick is no longer supported.
Power connection is by the of a standard barrel jack replacing the DIN connector.

This leaves substantial PCB real-estate, which is available for future use and evolution of this board

The Power (and Reset) buttons have been superseded with more available standardized components.
The original component footprints have still been left so can still install the original parts.

### Additionally

Additional changes have been made too numerous to mention please see [Changelog](/CHANGELOG.md) for details

## Advanced Features

What follows is specific guidance about certain features which come with consideration for
* The actual parts used that will need to be ordered
* The assembly of the components on the board itself 

### Alternate Main Clock

In V1-RevB (and latter) of the board, there is support for two types of main Clock
* A standard quartz crystal with 7404 circuit (the traditional design)
* A modern DIP-14 Can oscillator (discussed below)

A DIP-14 Can oscillator is a self-contained metal package (similar to normal quarts crystal)
that comes in a DIP-14 pinout, but only has 4 pins exposed.
* Pin 1 Enable
* Pin 7 Ground
* Pin 8 Main Clock TTL Level Output
* Pin 14 VCC

This component outputs a TTL level clock which is directly usable, without the need for any
external components. The existing circuit (and the 7404 pinout) has been designed so
the Oscillator can be installed in place of the 7404.
This means all the supporting circuitry (including the quartz crystal) can be removed.

A programmable oscillator is available from DigiKey, ("ECS-P145") and can exactly match
the required frequency, improving reliability, the part itself has not been tested.
Owing to height restrictions it is unlikely the oscillator could be socketed.

* https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-P145-AN/502317
* https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-P145-BX/965972
* https://www.ecsxtal.com/store/pdf/ecs-p143x-p145x.pdf

### Video Sync Timing

In V2 (and latter) of the board Video sync generation logic changed.

When assembling **maybe don't** install R16 and R18 until latter as these can be used 
to fine tune the Horizontal and vertical sync pulse durations.

tbd - info on setting up the timing signal's

### Joystick Port

In V2 (and latter) of the board a TRStick (Alpha) 5 bit Joystick Port was added. 
Note the port also supports a second fire button (6th bit),
but this would require a specific Joystick and software to use it.

The most important aspect is that the appropriate DB9 to 10 Pin header cable 
is ordered and attached as there are 2 incompatible types:
* Cross Wired (Correct)
* Straight Through (Incompatible)

You must use a Cross Wired cable, which maps the pins on the DB9 connector
based on the relative position, not the actual DB-9 pins. The easiest way to identify 
the correct cable is to purchase a cable with a DB-9 IDC connector. 
Cables that have a soldered connection (typically covered in a shroud)
can be wired in either configuration, and must be checked for compatability,
typically by removing the shroud.

See this guide which highlights the difference.
[Internal Serial Cables for COM2 Port](https://www.scantips.com/serial-db9.html)

### Amplifier and Speaker

In V2 (and latter) of the board

M1, M2, J8

