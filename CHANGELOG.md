
# Changelog

## Version 2.0 (Future)

Unreleased

### New Features

* Dual port video SRAM, reducing RAM contention (snow) issues
* Onboard Audio amplifier utilising small class D module, with space for PCB speaker
* Alpha Joystick port (5 bit) with header to connect 9 Pin Connector
* RGBtoHDMI full support by exposing HSYNC on video DIN
* Added Tim Halloran's no chip VBLANK modification  
* Added a pin Header (J19) next to CPU to expose /RD, /WR, and /M1 signals
  used for protocol decoding i.e. in Sigrok logic analyser
* Added support for EEPROM in circuit programing, enabled via JP30

### Changed Features

- Changed crystal oscillator to parallel resonant circuit based on 74HCU04 chip, 
  which has pin comparability with a Full Can (DIP14) oscillator.
- The Video DIN socket now has Jumper (JP19) to disable external power
- Moved main power switch (SW1) and connector (J11) slightly closer to other ports, for better case clearance
- Added Solder Jumper (JP16) to change the main Reset switch function from NMI to full CPU reset.
- Added PCB reset button (SW11) to allow full reset during diagnostics
- CPU speedup offer fast speed as 5.3 (default 3.55) mhz via jumper (JP17)
- Added Power LED indicator (D1) near to the main power switch.

### Minor Improvements  

- CPU clock selector flip flop (Z63a) clocked at slowest rate.
- Added resistor pull-ups on keyboard, prevent issues when no keyboard attached.
- Inputs of spare gates are now tied to GND or VCC, with easy trace cuts for future use.
- Removed remnants of CAS and MUX signals from IO expansion.
- Improved silkscreen for component IC identification
- Improved component identification in Bill of Materials
- C19, and C70 now use small electrolytic footprints
- Fixed multiple issues with small via's and thermal reliefs on power rails
- Main power Capacitor C101 now has more space for horizontal mounting.

## Version 1.0 (Current)

April 2025

![MainboardFrontBuiltK1](/images/IMG_8736.jpeg)

### New Features

* 48Kb RAM provided by a single static RAM chip (AS6C1008)
* System ROM's have been replaced with standard 32 pin 27xxx EPROM's or 28xxx EEPROM's
* System ROM's can be configured to occupy for 12 KB, 13 KB, or 14 KB of RAM.
* Video character generation is provided by standard 32 pin 27xxx EPROM's or 28xxx EEPROM's  
* Video character generation supports full (Gendon-3 compatible) descender's.
* Composite Video can be provided via standard RCA connector, replacing DIN connector
* All power regulation has been removed and requires an external regulated 5V DC power supply.
* Internal 40pin Expansion IO Header, located just behind the main expansion port
* Double Speed clock election (J18), auto fallback with cassette use

### Changed Features

* Power (and Reset) buttons have been superseded with more available standardized components
* Power connection is by the of a standard barrel jack replacing the DIN connector
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
