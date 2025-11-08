
# Changelog

## Version 2.0a (Current)

![MainboardFront](/pcb/TRS-80-MP-FrontV2a.png)

### Minor Improvements

This version was a minor patch after initial V2 prototype was created.
See the below for a list of all the version 2 changes
* Added testpoints to support 3 signals required by SuperMem
* Changed main power capacitor C11 to 470Uf after testing from MSly
* Changed main power switch to discharge C11 (using 100R R14) when switched off
* Keyboard resistor pack RN5 corrected to pull down keyboard data lines.
* Corrections to Bill of Materials, and silkscreen fixes and improvements.

## Version 2.0 (Past)

### New Features

* [Dual port video SRAM](FEATURES.md#video-ram), reducing contention (snow) issues with shared CPU access.
* [Onboard Audio amplifier](FEATURES.md#internal-audio-output) utilising small class D module, with space for PCB speaker
* [Alpha Joystick port](FEATURES.md#joystick-port) with header to connect 9 Pin DB9 Connector
* Changed crystal oscillator to parallel resonant circuit based on 74HCU04 chip,
  which is pin compatible with a [Full Can (DIP14) oscillator](FEATURES.md#alternate-main-clock).
* New [Video sync generation](FEATURES.md#video-sync-generation) circuit, including Horizontal and Vertical Position.
* Improved support for RGBtoHDMI by exposing HSYNC on Video DIN socket
* Added Tim Halloran's [no-chip VBLANK modification](FEATURES.md#video-output), for improved video updating. 
* Added Jumper (JP16) to allow main Reset button to function as full CPU reset.
* Can configure either RAM or ROM to occupy the 12kB to 14kB address space in memory.
* Added support for EEPROM in circuit writing (requires software support).

### Changed Features

- The Video DIN socket now has Jumper (JP19) to disable external power
- Added PCB reset button (SW11) to allow full reset during diagnostics
- CPU speedup offer fast speed as 5.3 (default 3.55) mhz via jumper (JP17)
- Added Power LED indicator (D1) near to the main power switch.
- Fixed issue with [TEST signal immediately disconnecting CPU from BUS](https://github.com/RetroStack/TRS-80-Model-I-Arduino-Library/blob/eeeaf3446552eadae234f6c2e0ac8c4adc224504/docs/TESTMod.md) - Credit Marcel Erz
- Fixed Issue with Bus control for interrupt Mode 0 and 2 where external device places data on bus
- Added (back) software character set control (Port FF Bit 7), as per JP board.
- Changed meaning of SW10-SW13. Now ON => Logic 1, and OFF => 0 (rather than reverse)
- RAM is configurable from $48k (default) down to 16k for compatability with external RAM.

### Minor Improvements  

- Moved main 10.6Mhz oscillator to central location, shorter signal paths.
- CPU clock speed selector flip-flop (U63a) clocked at slowest rate.
- JP10 (and related circuit) used for video frequency was removed.
- Inputs of spare gates are now tied to GND or VCC, with easy trace cuts for future use.
- Added resistor pull-ups on address, data, and control busses, for CMOS stability.
- Added resistor pull-ups on keyboard, prevent issues when no keyboard attached.
- Provided ability to use spare IO pins (CAS and MUX)  on IO expansion.
- Moved main power switch (SW1) and socket (J11) closer to other ports, better clearance
- Added several M3 mounting holes for internal expansion board mounting
- Improved (more modern) footprints for C19, C70, Q1, Q2, CR4.
- Replaced several discrete resistors with small resistor packs.
- Fixed multiple issues with small via's and thermal reliefs on power rails
- Main power Capacitor C101 now has more space for horizontal mounting.
- Improved silkscreen for component identification, and configuration options
- Improved component identification in Bill of Materials
- Major improvement in the Schematic diagram quality.
- Many component designators have changed from V1, so some V1 docs may not be accurate

## Version 1.0d (Future)

Unreleased

Fixes minor issues in version C
- Backported a V2 improvement to CPU clock speed selector flip-flop (Z63a) clocked at slowest rate.
- Added connection points (pads) for connecting supermem signals IN, OUT, and RESET.
- Legacy Power switch footprint, correct spacing of Pins to allow for install.
- Improve silkscreen to show what components can be removed when installing the alternate main clock
- Replace C101 which a 470uF, affects BOM only

## Version 1.0c (Current)

![MainboardFrontBuiltK1](/pcb/TRS-80-MP-FrontV1c.png)

This release fixes minor Issues
- Silkscreen for character generator SW10-SW13 has been corrected
- Added a single mounting hole, to allow for FreHD board to be mounted to.

## Version 1.0b (Past)

This is a patch version of the 1.0a board with the items back-ported from V2
- Z50 is now pin compatible with a [Full Can (DIP14) oscillator](FEATURES.md#alternate-main-clock).
- Inputs of spare gates are now tied a logic level, not left floating.
- Improved (more modern) footprints for C19, Q1, Q2, CR4.
- Fixed multiple issues with small via's and thermal reliefs on power rails
- Improved silkscreen for component identification, by moving labels under sockets

Also made following improvements, which were also included in V2
- Fixed issue with Excluded items in BOM JP21 JP27 J20
- Z6 component part numbers have been updated HCT -> LS throughout the project.
- Z31 component part numbers have been updated LS -> HCT throughout the project.
- Completed the BOM, with full part numbers.
- Improved edgecuts, especially around edge connector to support bevel

## Version 1.0a (Past)

8th August 2025

This is a patch version of the 1.0 board with the following issue (discovered during build) resolved

- An optional C61 (100pf) has been added connecting pins 5 to 7 of Z50. 
  It was discovered during initial testing (V1) to be needed get the main crystal oscillator to function.
  NOTE This **may not be required** in all circumstances.
- The main power connector (J11) GND pin thermal reliefs have been removed.
- Z32, Z50, and Z65 component part numbers have been updated throughout the project.
- C51 (duplicates C79) was removed.

## Version 1.0 (Past)

April 2025

### New Features

* 48Kb RAM provided by a [single static RAM chip](FEATURES.md#system-ram) (AS6C1008)
* System ROM's have been replaced with [standard 32 pin 27xxx EPROM](FEATURES.md#system-rom) or 28xxx EEPROM
* System ROM's can be configured to occupy for 12 KB, 13 KB, or 14 KB of RAM.
* Video [character generation](FEATURES.md#character-generation) is provided by standard 32 pin 27xxx EPROM's or 28xxx EEPROM's  
* Video character generation supports full (Gendon-3 compatible) descender's.
* Composite Video can be provided via [standard RCA connector](FEATURES.md#video-output), replacing DIN connector
* All [power regulation](FEATURES.md#power) has been removed and requires an external regulated 5V DC power supply.
* Internal [40pin Expansion IO Header](FEATURES.md#internal-expansion), located just behind the main expansion port
* [Double Speed clock](FEATURES.md#cpu) selection (J18), auto fallback with cassette use

### Changed Features

* [Power](PARTS_GUIDE.md#power-switch) (and [Reset](PARTS_GUIDE.md#reset-switch)) buttons have been superseded with more available standardized components
* [Power connection](PARTS_GUIDE.md#power-connector) is by the of a standard barrel jack replacing the DIN connector
* Pin Header for internal audio amplifier, taken from cassette output
* Pin Header for internal reset signal, mirroring the external reset switch
* This system is intended to be used (almost) exclusively with CMOS technology

### Minor Improvements  

The following additional changes were made:
- General replacement of wire jumpers with Pin Headers/Jumpers, or solder bridges
- Decoupling capacitors have been added throughout the board, on most IC's
- Full Ground Planes have been implemented, and Silkscreen has been modernised.
- RAM and ROM have been moved to the main data bus (previously memory data), leaving only keyboard on memory data.

Misc Circuit changes:
- Address decoding RAM/ROM logic has been changed, the circuit is different to the JP service manual
- JK Flip Flop Z63A (pins 1-6) was repurposed for CPU Speed control
- JK Flip Flop Z53A (pin 1-6) (previously part of Kana character generator) was used in place of Z62A
- U7 (dual 4 bit counter) replaces both Z7 and Z28 which were single counters
- U11 (8 bit latch) replaces Z11 (6 bit latch), moving other 2 data bits from Z56
- U24 (8 bit buffer) replaces Z24 (6 bit buffer), moving other 2 data bits from Z30
- U46 (quad nand) replaces Z46 (hex inverter)
- Z44 (quad nand) used in address decoder and video timing was removed
- Z39, Z55, and Z58 removed after consolidation of graphics into standard character generator
- Z62 and Z63 (partial) removed after removal of the DRAM timing circuitry

The above list may not be exhaustive
