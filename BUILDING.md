
# Builders Guide

## Provided Files

The files provided in this project are primarily:

- The Schematics in PDF Format [Schematics PDF Format](/pcb/TRS-80-MP-SchematicsV1b.pdf)
- Gerber files for manufacture [JLCPCB ZIP](/pcb/TRS-80-MP_JLCPCBV1b.zip) and [PCBWAY ZIP](/pcb/TRS-80-MP_PCBWayV1b.zip)
- Bill of Materials [BOM CSV Format](/pcb/TRS-80-MP-BillOfMatV1b.csv)
- A visual BOM is also available [VISUAL BOM](/pcb/TRS-80-MP-BomVisualV1b.html)
- The [Parts Guide](PARTS_GUIDE.md) for further advice on part usage
- The [Ordering](ORDERING.MD) guide for how to place a component order
- The [Known Issues](KNOWN_ISSUES.md) which identifies any deficiencies in the board itself
- The [Compatability Guide](COMPATABILITY.md) which identifies tested components and additions.

And the following
- A few compatible font have been provided in this project see [Fonts](/fonts/README.md)
- A few ROM image files have been provided in this project see [ROMS](/roms/README.md)
- A [FreHD board](/frehd/README.md) that can be connected directly to the mainboard, and installed internally.

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
- JP6, JP7, JP8, JP10 are required be configured as appropriate for either
  50Hz (PAL) or 60Hz (NTSC) video. You just need to solder a bridge on Pins 1&2 (NTSC) or 2&3 (PAL)
- Other solder jumpers can be changed at any time and have
  reasonable default connections. If changing you will probably need to cut existing connection

### Patches

Before beginning the main assembly you should understand the following limitations.

The following patches should be noted for the board. These were discovered after initial PCB manufacture, and affect
the boards design, and or the silkscreen. NOTE: The following have be fixed in V1a of the board.
- To get the main crystal oscillator to function a 100pf capacitor was installed connecting pins 5 to 7 of Z50
  - In latter revisions of the board C61 was added to the board to simplify this installation.

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
- Then all remaining ceramic disk capacitors.
  - These should all be 100nf (104) in value
  - There are approximately 50 of these.
  - While installing (using a Multimeter), please check the power rail is not shorted
- Install any IC sockets, preferably all IC's should be socketed. Don't install IC's at this point.
  - As a minimum you should have sockets for large scale components CPU,RAM,ROM, etc,
  - Some other more sensitive components Z3 (SN75452), Z25 (LM3900), Z50 (SN7404N)
- All Resistor Networks. These are labelled as RN1, RN2 on the PCB
- 4 way DIP Jumper Switch pack, SW10
- Main 10.6445 Mhz Quartz Crystal Y1.
  - If installing a tall component it must be mounted horizontally for height clearance
  - See section below additional/alternate installation.
- Jumper J18 - Should be shorted for normal CPU frequency
- Jumper JP21, JP27 - Needs to be jumpered to set the main ROM Chip Type
- Solder any optional Pin Headers (See Below)
- Cassette Relay K1
- Transistors Q1, Q2
- Power barrel Jack J11
- Electrolytic Capacitors C19, C70, and C101. 
  - These need to be installed in the correct polarity
  - The large capacitor (C101) should be mounted horizontally to reduce height
- Install all remaining electrolytic capacitors
  - These are all 10uF in value, and most are power decoupling
  - After installing (using a Multimeter), please check the power rails are not shorted
- Cassette DIN Socket J3
- Video output connector J2 (DIN) or J12 (RCA). 
  - If soldering DIN socket, don't solder (remove) the centre pin from the socket
- Main Power switch, solder either S1 (Traditional) or SW1 (Modern Toggle) switch.
- Main Reset switch, solder either S2 (Traditional) or SW2 (Modern) push button switch.
- Keyboard header CN3, Can be mounted on front (or  rear) of the PCB.
  - Should be mounted carefully depending on the cable connecting to the keyborard

## Assembly Options

What follows is specific guidance.

### Alternate Main Clock

The main board (V1-RevB and latter) supports two types of main Clock
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
- J20 - Used for installing an internal expansion card or ribbon cable. 
- J21 - Used to provide power to an internal expansion card.

## Testing

Before testing, you will need a regulated power supply that provides 5V. The connector is a center positive
barrel jack, and is quite common to find this connection in 12V power supplies, however these are not
compatible. The board performs no power regulation so a good quality power source is required.

**WARNING!!** - Connecting a 12V Power supply will probably **damage several components on the board**.
Please **test the power supply** for correct voltage and polarity **before connecting**.

For each of the step (when inserting components) ensure power is turned off and disconnected.
You will need to power on to perform necessary tests

Follow these steps
- Don't install any socketed IC's yet
- Before connecting power (using a multimeter) ensure the 5V and GND rails are not shorted
  - This can be done on any IC socket generally Pin's 14/16 and Pin's 7/8.  
- Connect the power supply to the board.
- With power turned off, test for +5V on J17, located just behind the barrel jack.
- With power turned on, test for +5V on a few IC sockets Pin 14 or 16 around the board.
- Insert all simple socketed logic chips
  - Including all 74xx series logic
  - Including Z3 (SN75452), and Z25 (LM3900)
  - Do not insert the CPU, ROMs, character generator, and RAMs for now.
- Use an oscilloscope test for a 1.77 Mhz Clock Signal on Pin 6 of the Z-80 CPU Socket
  - If not found then need to trace back to main oscillator
  - Consider installing C61 (Patch) to make main oscillator run.
- Connect a monitor (CRT preferable), you should see a video raster.
- Insert video generation chips
  - Static video RAM chips.
  - Insert character generator ROM.
- Ensure SW10 is configured for the chip type, and character set.
- When powered on you should see random but recognisable characters.
- With Power disconnected, Insert the main computer chips
  - Insert Z-80 CPU chip
- When powered on you should see the display fill up with repeating `@9`characters
  - This indicates the CPU is functioning and executing code.
- With Power disconnected, Insert the other chips
  - Insert main RAM chip
  - Install main ROM chip
- Ensure JP21, JP27 are configured for the ROM chip type you are using
- When powered on, you should see a prompt showing "MEM SIZE?" (if it is the normal system ROM).
  - You may see random characters being input, this is expected since keyboard is not connected
- Install the keyboard with the IDC cable (if you installed a header).
- Now, you should be able to use the system.

Additional Testing to consider:
- Load and save a program to cassette tape
- Run a Hello World program: 10 PRINT "Hello World!" (Return) 20 GOTO 10 (Return) RUN (Return).
  You should run this for some time. You can stop with the BREAK key.
- 32 character mode PRINT CHR$(xx) or right arrow and clear on the keyboard
- Another program to try ; 10 PRINT MEM;:IF MEM >100 GOSUB 10 ELSE RUN

## Troubleshooting

See [Troubleshooting Guide](./TROUBLESHOOT.md) for more information 

## Usage Notes

### FreHD

Consider building the separate [FreHD board](/frehd/README.md) for use with this board.

### Expansion Interface

When connecting the Expansion interface (EI) its internal RAM needs to be disabled.
Noting: It is not good enough to remove the RAM chips themselves, as regardless of the
presence of RAM, the EI buffers the output of RAM back to main databus.

There are 2 approaches:

(1) Remove (de-solder) the 74LS244 buffer chips Z29, and Z31, and replace with sockets. 
This completely isolates the RAM from the data-bus and is easily reversible by installing chips. 
The approach requires more work, but simple to change on the fly, and doesn't affect the circuit itself.
A future user will notice the missing chips and can simply install them to restore to factory
configuration.

(2) Disable the buffers from outputting back to the bus. There are 2 options that I can suggest
but without access to an expansion interface I am not sure which is easier;
* Cut trace leading out of Z28 Pin 6, and bridge Pin 19 of either Z29, or Z31 to Pin 20 (vcc)
* Cut trace leading into Z28 Pin 5, (or out of Z32 Pin 2) and bridge Z28 Pin 5 to Pin 7 (gnd)

The second approach requires less overall work, but is harder to revert. A future user will have
to trace out what was changed, and have skill to revert it.

