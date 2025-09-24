# FreHD for the Model 1

## Introduction

This is a project to provide a FreHD that directly connects to the TRS-80 Model 1 40 pin expansion port.
It was designed to be functionally compatible using primarily all the same parts, 
and also software compatible, as it uses he same PIC and GAL firmware

It was designed to work with the Model 1 attached via appropriate 40 pin ribbon cable,
and specifically for the Model 1k via it's internal expansion port,

The physical layout of the board while different still has the 
power and IO connection is on one side, and SD card and LED's on the other.
Mounting holes and some pinouts are different.

![3D Render](/frehd/images/Board3dRender.png)

### Improvements

The problematic 5V to 3.3V level shifter (Q1), and the voltage dividers implemented in resistors,
has been replaced with a small PCB module that provides level shifting and mounts in a 12 pin
DIP package. This package provides the appropriate transistors and resistors in SMT components.

The original design drove the WAIT bus signal (to high) preventing other peripherals to co-exist 
on the bus. A modification to the design allows for Open Collector output on the WAIT signal to resolve this.
To provide open collector a revised (different) version of the GAL firmware must be programmed, and Jumper J1 
on the board switched from 1-2 (default),to 2-3.

General improvements include, an optional onboard PCB reset pushbutton, full GND and Power planes, 
as well as more decoupling capacitors located (where possible) closer to chip VCC's

### Modifications

The J4 power connector may not have same pinout as modern (v1.3) FreHD. 

The J1 header for external LED's and Reset, has the pinout adjusted for direct compatibility with
microchip programmer ICSP pinout. If you 

The IOREQ signal provided to GAL has been removed and the GAL input tied to GND. 
It was determined that this signal was not required, as it duplicated RW/WR 
signals which were also present. This also mean that additional components
found on the Model 1 Hard disk adapter (transistors/resistors) that generated
this signal were also not required.

The RS232 capability has been omitted from the board.

See comments in the schematic for other modifications made.

## Building

### Files

The [pcb](./pcb) directory contains
* [PDF Schematics](./pcb/FreHD-SchematicV1.1.pdf), 
* Gerber files, and Bill of Materials.

### Parts

All parts (excepting PCB) are the same as the original excepting:

* (Sparkfun Quad Logic Level Converter Bidirectional)[https://www.sparkfun.com/sparkfun-logic-level-converter-bi-directional.html]
* (Memory Protection Devices BS7 Batter Holder)[https://www.memoryprotectiondevices.com/datasheets/BS-7/BS-7.pdf]

The other major original components are:

* (J2 - SD Card Socket - Hirose DM1AA-SF-PEJ.82)[https://au.mouser.com/datasheet/2/185/DM1AA_SF_PEJ_252872_2529_CL0609_0004_8_72_Catalog_-2585902.pdf]
* (U1 - PIC18F4620-IP microprocessor)
* (U2 - GAL16V8 PLD)
* (U4 - TS2950-3.3 voltage regulator)
* (U7 - DS1307 realtime clock)

### Assembly

The first step is probably to decide if you want the open collector WAIT signal,
requiring a reprogrammed GAL, if so you need to Cut JP1 1,2 and solder 2 to 3
If you think you may want to change this in the future, it may be easier to cut
the trace and solder 1 to 2 now, making it easier to change in the future.

Note: Unless you need this it may be safer to stick with the default, as may cause 
confusion latter, if the GAL needs replacing, have to ensure the modified firmware is programmed.

The next step is to solder the SMD SD card, followed by the through hole components.

As a minimum sockets need to be installed for PIC and GAL, so they can be reprogrammed.
IC sockets are preferred on other components e.g. RTC, and 7400 series logic so they 
can be replaced but it is not strictly essential.

Solder components typically in size and height order, typically from the lowest profile to highest, 
and from smallest to largest. The only exception is the small crystal oscillator, 
it is sensitive to damage, maybe consider soldering it latter.
The 12 pin level shifter can be soldered using small short pin headers.

### Optional Parts

If required you can choose to solder one of of the following options.
The first option is typically the default. 

Power connection is via 1 of 2 header sockets.
* J4 - Providing VCC and GND via similar header to the original board.
* J6 - Designed for use with the modern TRS-80 Model 1k (evolution) internal expansion port.
  Providing VCC only, GND comes from he 40 pin IO connector

Dual sets of onboard LED's are provided, maximum of one of either:
* Populate - D11, D12, R33, R34 - for mounting on the front on the PCB
* Populate - D1, D2, R13, R14 - for mounting on the rear on the PCB
* External LED's via J1

Optional external Programming Header:
* J1 - for external PIC programming, OR external reset and LED's

Optional reset for the PIC:
* SW1 - for onboard reset pushbutton

## Programming

The PIC must be programmed. The latest release is 2.17 and is in the file "FATFS.HEX"
* The original PIC [FreHD PIC](https://github.com/veco/FreHDv1/tree/main/sw/trs_hard)

The GAL must be programmed. There are 2 versions
* The original GAL [FreHD GAL](https://github.com/veco/FreHDv1/tree/main/hw/gal)
* The modified GAL [Open Collector GAL](https://github.com/maboytim/FreHDv1/tree/main/hw/gal-oc)

## Additional

Additional Images can be found here [Images](./images/README.md)

## Resources

The use of the FreHD is not well documented, see [Resources](./RESOURCES.md)

## Credits

The original designer without which this project would not be possible

maboytim - for support in coming up with open collector design on the WAIT bus signal,
and for investigating the use of IOREQ signal and its use in the GAL logic.
