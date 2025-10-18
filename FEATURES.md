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

A selectable 2/3 clock speedup (3.5Mhz/5.3Mhz) mod has been applied. A jumper (J18) allows the clock to be slowed to normal.
This could be by external switch, or any future circuit potentially under software control.
Note: If the cassette motor is turned on the speed will automatically be slowed.

The Reset Switch can now be changed from a soft NMI Reset to a hard CPU Reset. Also, an onboard hard
reset is provided via pushbutton, for full reset during diagnostics

### System ROM

Uses a standard 27xxx EPROM (or 28256 EEPROM) rather than mask ROM. These are more readily available and easier to program.
The two ROM's (Z42, Z43) have been replaced with a single 28 pin EPROM (U42) supporting 2x128 thru 2x512 chips.
The board has jumpers to configure the ROM type, and/or 16kB page used for larger ROMS.

An additional set of jumpers allows either ROM (or RAM) to be mapped in the memory address
above the normal ROM (0x3000 - 0x37FF). This can be useful for custom ROM extensions,
commonly used on some Model 1 peripherals, or RAM for any purpose

### System RAM

The 4116 16kb DRAM has been replaced with a single static RAM chip (AS6C1008) providing 48KB of RAM without the
need for an external expansion interface or other add on card. Note this chip is 128 kBytes in size, but only 48kB
is being used. No provision for RAM paging has been made.

An optional add-on board provide [SuperMem 512KB](/supermem/README.md) banked RAM support

If you intend to connect an expansion interface then the RAM in the interface will have to be disabled to prevent conflict.

### Video RAM

One of the bigger issues with model 1 design was use of shared video ram with very primitive contention resolution.
The Model 1 video subsystem takes second priority to CPU, causing artefacts (snow) when CPU accesses video RAM during visible period.
The Model 3 somewhat improved this by asking CPU to wait for next blank interval, giving priority to video system.

In V2 of the board a Dual Port video SRAM was added
- The chip itself has 2 channels/ports, mirroring all address data control lines as if a standalone chip. This accounts for the chips high 48 pin count
- Contention still exists but this is at byte level, Ie when both ports try to access the same address in RAM
- This significantly reduces the chance of contention when CPU accesses vram from about 33% (time when not blanking), to about  .033% a factor of 1024
- When contention occurs the second request (CPU or video side) receive a Busy signal, this as handled on the CPU side big signaling a WAIT. On the video side the existing logic is used, displaying artifacts.
- Chip count and complexity is reduced by removing address multiplexes, and data buffer to main data bus. From 6 (including 2 Ram chips) to single RAM large chip

### Character Generation

All character generation (both alpha characters and graphics) has been replaced with a single character set
that includes all 256 characters defined in ROM (U37). Each character defines the full 6x12 pixel matrix that is
generated. This approach is identical to the Gendon3 Model 1 font upgrade, and supports full lower case descenders.
The fonts used are compatible with Glens Stuff TRS-80 Model 1 Clone.

Each character requires 16 bytes (12 bytes used) per character, for a total of 4k bytes for the entire 256 character set.
Multiple character sets  can be defined (depending on ROM size), the character set chosen is configured by onboard dip switches.
Also Port FF Bit 7 can be used to control the LSB of the character set selection

A selection of [fonts files](/fonts/README.md) for use with this project. Normal font ROM's are not compatible.

### Video Output

Composite video output is via the original DIN plug, or an optional RCA connector, you can solder either onto the board.
The RCA connector is provided to be compatible with a larger range of external monitors, potentially more reliable and
less subject to noise.

A modern video sync generation circuit exists 
* In V1 (of this board) it used the Japanese design, which derived sync pulses directly from the main counters
* In V2 a new design was introduced, See the section [Video Sync Generation](#video-sync-generation) for more details

If using the DIN socket better support has been added to allow the use of RGBtoHDMI, by passing the HDRV signal to
pin 3 of the DIN socket. This is enabled by bridging jumper JP15. See below for further details.
* https://github.com/hoglet67/RGBtoHDMI/wiki/Cables#trs80-model-1-mono--video-genie

For tear free video output Tim Halloran's no chip VBLANK modification is provided. See following for details:
* https://github.com/hallorant/bigmit/blob/master/ta19demo/README.md

### Internal Expansion:

The main board has an internal 40pin Header (J20) identical to and located just behind the main 40 pin expansion port.
This is primarily designed for an internal expansion board which sits inside the case.
The primary advantage being compactness. A optional second connector provides +5V in a four pin header (J21) for powering
a internal expansion board.
A few additional mounting holds have been provided to support an addon board

See the [FreHD folder](/frehd/README.md) for a 40 pin FreHD that connects directly to this header.

Routing an external 40 pin ribbon cable to the connector is also possible, bypassing the 'unreliable' card edge connector.

Also provided for expansion are:
- Pin Header (J14) for internal reset signal, mirroring the external reset switch, SW11 also provides PB switch
- Pin Headers (J15,J16) are for internal 5V power for any other devices
- Pin Headers (J17) for internal (un-switched) +5V (both pins) power, for any devices requiring constant power

NOTE: The DRAM multiplexing signals CAS, and MUX are no longer generated, and have be removed on the main expansion connector.
These two expansion pins can be re-used for any future purpose, they are exposed as solder pads on the PCB

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

### Video Sync Generation

First some History:

* The traditional Model 1 - used 74C04 CMOS inverters to build an analog timing circuit.
  This circuit was **highly** problematic and known to fail over time.
* The Japanese Model 1 (which this board is derived) used a digital sync signal derived off the 
  primary video counter/dividers. This meant rock steady sync but eliminated picture adjustment  

In V1 of this board the Japanese design was followed. In V2 a new design was introduced
The rest of this section describes this approach.

The new (V2) design uses specific monostable multi-vibrators (74221) controlled by an RC network.
This approach was partially used in the Model 3, and fully used in "Glens stuff TRS-80 Model 1 clone"

This design allows for calibration of both 
* the sync pulse delay (H and V position), is done via trim pots (RV4, RV5). 
* the sync pulse duration via fixed trimming resistors (R16, and R18).  

See the Section [Video Calibration](./CONFIG.md#video-calibration) which covers this
process to perform calibration of the video circuitry.

### Joystick Port

In V2 (and latter) of the board a TRStick (Alpha) 5 bit Joystick Port was added.
At this time 4 bit mode is not supported.
The port also supports a 6th bit, (second fire button),
but this would require a specific Joystick and software to use it.

The most important aspect is that the appropriate DB9 to 10 Pin header cable 
is ordered and attached as there are 2 incompatible types:
* Cross Wired (Correct)
* Straight Through (Incompatible)

You must use a Cross Wired cable, which maps the pins on the DB9 connector
based on the relative position, not the actual DB-9 pin numbering. 
The incompatible) straight through cable in contrast ensures the 
pin numbering on the DB-9 matches the pin numbering on the pin header

The easiest way to identify the correct cable is one with a DB-9 IDC connector. 
Cables that have a soldered connection (typically covered in a shroud)
can be wired in either configuration, and must be checked for compatability,
typically by removing the shroud.

See this guide which defines and highlights the difference.
[Internal Serial Cables for COM2 Port](https://www.scantips.com/serial-db9.html)

### Internal Audio Output

In V2 of the board, and onboard amplifier (module) and small speaker is supported
A volume control is provided (RV2), with a speaker needing to be attached to (J8)
If supported the amplifier will be muted when the cassette interface is active.

#### Amplifier

A small 6 pin amplifier module based on either LTK5128, or (identical) XPT8871 chipset is used
For more information about the chip itself. Noting datasheets are in chinese
* https://components101.com/ics/XPT8871-audio-amplifier-ic-pinout-datasheet-circuit

Googling these chip ID's you will find the modules themselves. There are three variants
which differ in pcb colour/size, pinout, and main capacitor size.
They are commonly available from online chinese stores, or ebay.

There are 2 pin outs supported. Which are identified as M1, and M2 on the main PCB. 

| Module | Height/Width | Pinout                            |
|--------|--------------|-----------------------------------|
| M1     | 16mm x 20mm  | +5V, GND, GND, Input, Out+, Out-  |
| M2     | 16mm x 12mm  | Out+, Out-, Mute, GND, Input, +5V | 

Note: M2 offers a Mute function, which is activated when the cassette motor is on.

Three modules are typically available

| PCB Colour | Module | Feature                                  |
|------------|--------|------------------------------------------|
| Red        | M1     | Large 470uF thru-hole power capacitor    |
| Green      | M1     | Medium 220uF thru-hole power capacitor   |
| Blue       | M2     | Small 100uF SMD capacitor, supports Mute |

When purchasing this you should probably get one without a soldered header.
The module is designed to be mounted with the components facing up.

#### Speaker

The amplifier module supports a small speaker, typically about 5 watts.
You are free to support any speaker and mount it inside the case, connecting it to 
the J8 pin header on the main PCB

Alternately a small speaker can be mounted to the PCB itself, there is a space 
for a 60mm (radius) or 45mm x 45mm (square) speaker. Mounting could be 
by hot glue, or by double-sided tape, or another method
