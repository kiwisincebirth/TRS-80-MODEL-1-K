
# Builders Guide

## Provided Files

The files provided in this project are primarily:

- The Schematics in PDF Format [Schematics PDF Format](/pcb/TRS-80-MP-SchematicsV1b.pdf)
- Gerber files for manufacture [JLCPCB ZIP](/pcb/TRS-80-MP_JLCPCBV1b.zip) and [PCBWAY ZIP](/pcb/TRS-80-MP_PCBWayV1b.zip)
- Bill of Materials [BOM CSV Format](/pcb/TRS-80-MP-BillOfMatV1b.csv)
- A visual BOM is also available [VISUAL BOM](/pcb/TRS-80-MP-BomVisualV1b.html)
- Also see the [Parts Guide](PARTS_GUIDE.md) for further advice on part usage
- Also see the [Ordering](ORDERING.MD) guide for how to place a component order
- Also see the [Known Issues](KNOWN_ISSUES.md) which identifies any deficiencies in the board itself

And the following
- A few compatible font have been provided in this project see [Fonts](/fonts/README.md)
- A few ROM image files have been provided in this project see [ROMS](/roms/README.md)

## Introduction

The PCB is flexible and allows certain the installation of either Modern or Traditional components this includes
* The main power switch either Traditional, or modern toggle switch
* The video output either traditional DIN, or RCA connector
* Note: The traditional DIN power connector is NOT supported

Other components that can be substituted are
* Main System ROM, and character generator ROM support 27128, 27256, 27512, or 28256

Before starting, you should ensure you have read and understand all the documentation
You should also have assembled all the components you need

## Pre Assembly

### Programming ROMS

You will also need to program the two (E)EPROMS, the Main system ROM, and the Character generator ROM.
You will need an apprpriate programmer to do this.

For the main system ROM you should use the latest 1.3 version of the L2 ROM's
Some ROM images have been provided in the ROMS folder.

For the Character generator ROM you may include multiple character fonts
and choose which font via DIP switches. See the FONTS folder for these images

### Solder Jumpers

Before starting need to look at the solder jumpers on the board.
- JP6, JP7, JP8, JP10 on the board are required be configured as appropriate for either
  50Hz (PAL) or 60Hz (NTSC) video. You just need to solder a bridge on Pins 1&2 or 2&3
- Other solder jumpers on the board can be changed at any time and have
  reasonable default connections. If changing you will probably need to cut existing connection

### Patches

Before beginning the main assembly you should understand the following limitations.

The following patches should be noted for the board. These were discovered after initial PCB manufacture, and affect
the boards design, and or the silkscreen. NOTE: The following have be fixed in V1a of the board.
- To get the main crystal oscillator to function a 100pf capacitor was installed connecting pins 5 to 7 of Z50

Additionally, please see the [Known Issues](./KNOWN_ISSUES.md) which describe issues with the board design itself,
that should also be addressed during build.

## Main Assembly

Most components are labeled on the PCB, as you install each component you should check its value
against what is in the BOM, and cross it off. An interactive BOM is provided to aid in this process

Typically, solder components in order of the lowest profile to the tallest components.
- All resistors, these can be installed in either direction as they do not have a polarity.
  - Note R37 is a 1/2 watt resistor and slightly bigger than the other resistors.
- Diodes, fitting CR5-CR8 (1N4148), and then CR4 (1N4001) last
- Ceramic disk capacitors with specific values 
  - C3, C13, C17, C18, C43, C48, C50, C57, C60
- Then all remaining (Decoupling) 100nf (104) ceramic disk capacitors. 
  - There are approximately 50 of these.
- Install any IC sockets, preferably all IC's should be socketed. Don't install IC's at this point.
  - As a minimum you should have sockets for large scale components CPU,RAM,ROM, etc,
  - Some other more sensitive components Z3 (SN75452), Z25 (LM3900), Z50 (SN7404N)
- All Resistor Networks. These are labelled as RN1, RN2 on the PCB
- 4 way DIP Jumper Switch pack, SW10
- Main 10.6445 Mhz Crystal Y1. (See Below).
- Jumper J18 - Should be shorted for normal CPU frequency
- Jumper JP21, JP27 - Needs to be jumpered to set the main ROM Chip Type
- Solder any optional Pin Headers (See Below)
- Cassette Relay K1
- Transistors Q1, Q2
- Power barrel Jack J11
- Electrolytic Capacitors C19, C70, C101. 
  - These need to be installed in the correct polarity
- Install remaining Electrolytic Capacitors, these are all 10uF in value
- Cassette DIN Socket J3
- Video Output J2 or J12. If soldering DIN socket, don't solder (remove) the centre pin.
- Main power switches, solder either SW1 or S1,
- Main Reset switch solder either SW2 or S2
- Keyboard header CN3, on front (or  rear) of the PCB.

## Assembly Options

What follows is specific guidance.

### Main Clock

tbd info on alternate installation

M1, M2, J8

### Legacy Connectors

tbd info on installing modern vs legacy connections

### Power Connector

tbd info on regulated PSU and cable, maybe about using USB

## Configuration

Configuration is provided by several jumper options
- JP6, JP7, JP8, and JP10 - (REQUIRED) - Used to configure video output to either 50Hz or 60Hz.
- JP13, JP14 - Size of the main system ROM as either 12KB (DEFAULT), 13KB, or 14KB
  - Note : 1&2 are bridged by default and need to be cut for any change.
  - Note : Using a 14KB ROM size will prevent the use of Model 1 floppy controller or printer port which occupy
    memory in the 0x37E0 - 0x37FF range. If using a 14kb ROM the 0x37E0 - 0x37EF memory address should probably
    return 0xFF so (if installed) a Level 2 ROM will not think a floppy controller is attached.
- JP21, JP27 - (REQUIRED) - Configures the type and Page of the main ROM. 
  - Note : JP21 controls Pin 21, and JP27 controls Pin 27
  - Note : Shorting Pin 1&2 = Logic 1 , while shorting Pin 2&3 = Logic 0
- SW10 - SW13 - (REQUIRED) - Configures the Character generator ROM
  - Note : See silkscreen for details of this.
  - Note : The switch polarity is reversed Switched On = Logic 0, Switched Off = Logic 1
- J18 - Short pin to set CPU speed to Normal 1.77Mhz, or removed for 2x speed.
  - This can be routed to a switch, which could use a small capacitor to avoid bounce

## Optional Headers

The following optional headers Pins are provided, you can choose to install or not install as required
- J13 - Audio signal taken from cassette output, requires an amplifier
- J14 - Used to connect an external reset button, mirroring the external reset switch
- J15, J16 - are pin headers that provide 5v power for any internal board or accessory
- J17 - an alternate way to supply (or use) 5V power (both pins) to the board. This is before the power switch
- J20 - Used for installing an internal expansion card or ribbon cable. J21 provides power to an internal card.

## Testing

For each of the step (when inserting components) ensure power is turned off and disconnected.
You will need to power on to perform necessary tests

Follow these steps
- Don't install any socketed IC's yet
- Connect a regulated 5V supply to the board.
- With power turned off, test for +5V on J17, located just behind the barrel jack.
- With power turned on, test for +5V on a few IC sockets Pin 14 or 16 around the board.
- Insert all simple socketed logic chips
  - Including all 74xx series logic
  - Including Z3 (SN75452), and Z25 (LM3900)
  - Do not insert the CPU, ROMs, character generator, and RAMs for now.
- Use an oscilloscope test for a 1.77 Mhz Clock Signal on Pin 6 of the Z-80 CPU Socket
- Connect a CRT (preferable) monitor, you should see a video raster.
- Insert video generation chips
  - Static video RAM chips.
  - Insert character generator ROM.
- Ensure SW10 is configured for the chip type, and character set.
- When powered on you should see random but recognisable characters.
- With Power disconnected, Insert the main computer chips
  - Insert Z-80 CPU chip
  - Insert main RAM chip
  - Install main ROM chip
- Ensure JP21, JP27 are configured for the ROM chip type you are using
- When powered on, you should see a prompt showing "MEM SIZE?" (if it is the normal system ROM).
  - You may see random characters being input, this is expected since keyboard is no connected
- Install the keyboard with the IDC cable (if you installed a header).
- Now, you should be able to use the system.

Additional Testing to consider:
- Load and save a program to cassette tape
- Run a Hello World program: 10 PRINT "Hello World!" (Return) 20 GOTO 10 (Return) RUN (Return).
  You should run this for some time. You can stop with the BREAK key.
- 32 character mode PRINT CHR$(xx) or right arrow and clear on the keyboard
- Another program to try ; 10 PRINT MEM;:IF MEM >100 GOSUB 10 ELSE RUN

