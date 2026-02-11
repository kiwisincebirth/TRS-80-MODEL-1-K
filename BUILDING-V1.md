
# Builders Guide (V1)

This Guide is for **VERSION 1** of the board.
For the current V2 please see the [Builders Guide V2](/BUILDING.md)

## Provided Files

The files provided in this project are primarily:

- The Schematics in PDF Format [Schematics PDF Format](/pcb/TRS-80-MP-SchematicsV1d.pdf)
- Gerber files for manufacture [JLCPCB ZIP](/pcb/old/TRS-80-MP_JLCPCBV1d.zip) and [PCBWAY ZIP](/pcb/old/TRS-80-MP_PCBWayV1d.zip)
- Bill of Materials [BOM CSV Format](/pcb/TRS-80-MP-BillOfMatV1d.csv)
- A visual BOM is also available [VISUAL BOM](/pcb/TRS-80-MP-BomVisualV1d.html)
- The [Ordering](ORDERING.MD) guide for how to place a component order
- The [Parts Guide](PARTS_GUIDE.md) for further advice on part usage
- The [Known Issues](issues/KNOWN_ISSUES.md) which identifies any deficiencies in the board itself
- The [Compatability Guide](COMPATABILITY.md) which identifies tested components and additions.

And the following
- A few compatible font have been provided in this project see [Fonts](/fonts/README.md)
- A few ROM image files have been provided in this project see [ROMS](/roms/README.md)
- A [FreHD board](/frehd/README.md) that can be connected directly to the mainboard, and installed internally.
- A [Floppy80 board](/floppy80/README.md) that can be connected directly to the mainboard, and installed internally.
- A [SuperMem 512](/supermem/README.md) board that replaces the System RAM board providing 512KB of banked RAM

## Introduction

The PCB is flexible and allows certain the installation of either Modern or Traditional components this includes
* The main power switch either Traditional, or modern toggle switch
* The video output either traditional DIN, or RCA connector
* Note: The traditional DIN power connector is **NOT** supported

Other components that can be substituted are
* Main System ROM, and character generator ROM support 27128, 27256, 27512, or 28256
* Main System RAM can be enhanced with [SuperMem 512](/supermem/README.md) compatible banked RAM
* An [Alternate Main Clock](./FEATURES.md#alternate-main-clock) provides support
  for a modern Can Crystal oscillator, rather than traditional discrete crystal circuit.

* Before starting, you should ensure you have read and understand all the documentation
You should also have assembled all the components you need

## Pre Assembly

### Programming ROMS

You will also need to program the two (E)EPROMS, the Main system ROM, and the Character generator ROM.
You will need an appropriate programmer to do this.

For the main system ROM you should probably use the latest 1.3 version of the 
L2 ROM's. Some ROM images have been provided in the [ROMS](./roms/README.md) folder.

For the Character generator ROM you may include multiple character fonts
and choose which via DIP switches. See the [FONTS](./fonts/README.md) folder for these images

### Solder Jumpers

Before starting need to look at the solder jumpers on the board.
- JP6, JP7, JP8, JP10 are required be configured as appropriate for either
  50Hz (PAL) or 60Hz (NTSC) video. You just need to solder a bridge on Pins 1&2 (NTSC) or 2&3 (PAL)
- Other solder jumpers can be changed at any time and have
  reasonable default connections. If changing you may need to cut the existing connection.

### Patches

Before beginning the main assembly you should understand the following limitations.

The following patches should be noted for the board. These were discovered after initial PCB manufacture, and affect
the boards design, and or the silkscreen. NOTE: The following have be fixed in V1a of the board.
- To get the main crystal oscillator to function a 100pf capacitor was installed connecting pins 5 to 7 of Z50.
  In latter revisions of the board C61 was added to the board to simplify this installation.
- There is an [issue with CPU Frequency selection](./issues/FIX_CPU_SPEED.md), requiring a change. For Rev C boards traces need to be
  cut before the board is assembled.

Additionally, please see the [Known Issues](issues/KNOWN_ISSUES.md) which describe issues with the board design itself,
that should also be addressed during build.

## Main Assembly

Most components are labeled on the PCB, as you install each component you should check its value
against what is in the BOM, and cross it off. An interactive BOM is provided to aid in this process

Typically, solder components in order of the lowest profile to the tallest components.
- All resistors, these can be installed in either direction as they do not have a polarity.
  - Note R37 is a 1/2 watt resistor and slightly bigger than the other resistors.
- Next install diodes, fitting CR5-CR8 (1N4148), and then CR4 (1N4001) last
- Then install ceramic disc capacitors with specific values
  - C3, C13, C17, C18, C43, C48, C50, C57, C60
- Then install all remaining (power decoupling) ceramic disk capacitors.
  - There are about 50 of these and are all 100nf (104) in value.
  - While installing (using a Multimeter), please check the power rails are not shorted
- Install IC sockets, (preferably) for all IC's. Don't install IC's at this point.
  - As a minimum you should have sockets for large scale components CPU,RAM, etc.
  - You MUST install sockets for ROM's, including the character generator.
  - Consider sockets for more sensitive components Z3 (SN75452), Z25 (LM3900)
  - If installing the [Alternate Main Clock](./FEATURES.md#alternate-main-clock) DON'T install socket for Z50
  - If installing the [SuperMem](/supermem/README.md) board consider not installing a socket System RAM
- 4 way DIP Jumper Switch pack, SW10
- All Resistor Packs. These are labelled as RNxx on the PCB.
- Main 10.6445 Mhz Quartz Crystal Y1.
  - If installing a tall component it must be mounted horizontally for height clearance
  - If installing a [Alternate Main Clock](./FEATURES.md#alternate-main-clock) DON'T install Y1
- Electrolytic Capacitors C19, C70, and C101.
  - These need to be installed in the correct polarity
  - The large capacitor (C101) should be mounted horizontally to reduce height
- Then install all remaining electrolytic capacitors.
  - These are all 10uF in value, and most are power decoupling.
  - While installing (using a Multimeter), please check the power rails are not shorted
- Jumper J18 - Should be shorted for normal CPU frequency
- Jumper JP21, JP27 - Must be jumpered to set the main ROM Chip Type
- Solder any [Optional Pin Headers](#optional-headers)
- Cassette Relay K1
- Transistors Q1, Q2
- Power barrel Jack J11
- Cassette DIN Socket J3
- Video output connector J2 (DIN) or J12 (RCA). 
  - If soldering DIN socket, don't solder (remove) the centre pin from the socket
- Main Power switch, solder either S1 (Traditional) or SW1 (Modern Toggle) switch.
- Main Reset switch, solder either S2 (Traditional) or SW2 (Modern) push button switch.
- Keyboard header CN3, Can be mounted on front (or  rear) of the PCB.
  - Should be mounted carefully depending on the cable connecting to the keyborard

Once assembled it is recommended that the board be cleaned of any resin/flux
deposited during soldering. Using a soft toothbrush and isopropyl alcohol is generally
acceptable for this process.

## Assembly Options

Please see the Section [Advanced Feature](./FEATURES.md#advanced-features)
which describes some additional assembly information, and includes some information
about additional parts that may be required.

## Configuration

Configuration of the board is via [Jumpers](./CONFIG.md#version-1-jumpers)

## Optional Headers

The following optional headers Pins are provided, you can choose to install or not install as required
- J13 - Audio signal taken from cassette output, requires an amplifier
- J14 - Used to connect an external reset button, mirroring the external reset switch
- J15, J16 - are pin headers that provide 5v power for any internal board or accessory
- J17 - an alternate way to supply (or use) 5V power (both pins) to the board. This is before the power switch
- J20 - Used for installing an internal expansion card or ribbon cable.
- J21 - Used to provide power to an internal expansion card.

## Initial Testing

See [Testing Guide](./TROUBLESHOOT.md) for more information

## Troubleshooting

See [Troubleshooting Guide](./TROUBLESHOOT.md) for more information

## Usage Notes

See [Compatability Notes](./COMPATABILITY.md)
