
# Builders Guide

For V1 please see the [Builders Guide V1](/BUILDING-V1.md)

## Provided Files

The files provided in this project are primarily:

- The Schematics in PDF Format [Schematics PDF Format](/pcb/TRS-80-MP-SchematicsV2.pdf)
- Gerber files for manufacture [JLCPCB ZIP](/pcb/TRS-80-MP_JLCPCBV2.zip) and [PCBWAY ZIP](/pcb/TRS-80-MP_PCBWayV2.zip)
- Bill of Materials [BOM CSV Format](/pcb/TRS-80-MP-BillOfMatV2.csv)
- A visual BOM is also available [VISUAL BOM](/pcb/TRS-80-MP-BomVisualV2.html)
- Also see the [Parts Guide](PARTS_GUIDE.md) for further advice on part usage
- Also see the [Ordering](ORDERING.MD) guide for how to place a component order
- Also see the [Known Issues](KNOWN_ISSUES.md) which identifies any deficiencies in the board itself

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

The PCB has clear instructions for components considered (Optional). If you don't need a feature
or wish to install it latter you can simply exclude it. Note however the components are included in the BOM
* Cassette interface for loading/reading programs. Excluding these components does not prevent Audio output.
* The cassette relay can also be excluded, which only prevents to control of external tape drive
* The joystick interface is also optional and can be excluded
* Audio amplifier and speaker are not required
* This also includes many Pin Headers which are for external connection.

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

Before starting need to look at the solder jumpers on the rear of the board.
- JP6 is required be configured as appropriate for either
  50Hz (PAL) or 60Hz (NTSC) video. You just need to solder a bridge on Pins 1&2 (NTSC) or 2&3 (PAL)
- Other solder jumpers can be changed at any time and have
  reasonable default connections. If changing you may need to cut the existing connection

### Patches

Before beginning the main assembly you should understand the following limitations.

The following patches should be noted for the board. These were discovered after initial PCB manufacture, and affect
the boards design, and or the silkscreen.
- nothing known at this time.

Additionally, please see the [Known Issues](./KNOWN_ISSUES.md) which describe issues with the board design itself,
that should also be addressed during build.

## Main Assembly

Most components are labeled on the PCB, as you install each component you should check its value
against what is in the BOM, and cross it off. An interactive BOM is provided to aid in this process

Typically, solder components in order of the lowest profile to the tallest components.
- All resistors, these can be installed in either direction as they do not have a polarity.
  - Note R37 is a 1/2 watt resistor and slightly bigger than the other resistors.
  - Resistor values are labelled on the board using R (ohms) K (kOhms) M (mOhms)
- Diodes, fitting CR5-CR8 (1N4148), and then CR4 (1N4001) last
- Ceramic disc capacitors with specific values
  - C3, C5, C6, C7, C8, C13, C17, C18, C43, C48, C50, C57, C60, C61
  - Capacitors are labelled on the board in 3 digit (value exponent) notation
- Then all remaining ceramic disk capacitors.
  - These should all be 100nf (104) in value
  - There are approximately 50 of these.
  - While installing (using a Multimeter), please check the power rail is not shorted
- Install any IC sockets, preferably all IC's should be socketed. Don't install IC's at this point.
  - As a minimum you should have sockets for large scale components CPU,RAM,ROM, etc,
  - Some other more sensitive components U3 (SN75452), U25 (LM3900), U60 (74HCU04)
- All Resistor Packs. These are labelled as RPxxx on PCB and clearly indicate the value
- 4 way DIP Jumper Switch pack, SW10
- Main 10.6445 Mhz Quartz Crystal Y1.
  - If installing a tall component it must be mounted horizontally for height clearance
  - See section below additional/alternate installation.
- Onboard Power LED D1. It needs to be installed in the correct polarity
  - This is optional, and can be installed at any time.
- Jumper J18 - Should be shorted for normal CPU frequency
- Jumper JP21, JP27 - Needs to be jumpered to set the main ROM Chip Type
- Solder any optional Pin Headers (See Below)
- Cassette Relay K1
- Transistors Q1, Q2
- Power barrel Jack J11
- RV2, RV4, RV5 Trim resistors. The alignment should be clear on the silk screen.
- Electrolytic Capacitors C11, C19, C70.
  - These need to be installed in the correct polarity
  - The large capacitor (C11) should be mounted horizontally to reduce height
- Install all remaining electrolytic capacitors
  - These are all 10uF in value, and most are power decoupling
  - After installing (using a Multimeter), please check the power rails are not shorted
- Cassette DIN Socket J3
- Video output connector J2 (DIN) or J12 (RCA).
  - If soldering RCA be sure to bridge solder jumper JP20.
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

### Video Timing

tbd - info on setting up the timing signal

### Amplifier and Speaker

M1, M2, J8

### Joystick Port

J9 and cable

## Configuration

Configuration is provided by several jumper options
- JP6 - (REQUIRED) - Used to configure video output to either 50Hz or 60Hz.
- JP10 - Configure how character generator selects its page number (LSB), switch vs software.
  - Note : 1&2 are bridged by default, using SW13 to select the LSB char generator page
  - Note : Setting 2&3 enable software selection using (Port FF Bit 7), ignoring SW13.
- JP12 - Configure the use of an all RAM machine, replacing the use of ROM. This is provided
  as an experimental feature, a boostrap process will be needed to initialise the computer
  - Note : If shorting this the ROM chip itself should be removed.
  - Note : If shorting this JP14 (1&2) cannot be bridged, instead (2&3) must be used.
- JP13, JP14 - Configure either RAM or ROM to be mapped into the 12-13kb and 13-14kb address space
  - Note : Using the 13-14kb address space will prevent the use of Floppy disk
    or printer which occupy memory in the 0x37E0 - 0x37FF range.
  - Note : If using the 13-14kb address space unmodified Level 2 ROM may cause issues.
    I have included modified ROMs to deal with these issues.
- JP15 - Enable output of HDRV on Video DIN socket for RGBtoHDMI support
  - Note : Only bridge this if installing DIN connector, RCA connector can't use it
- JP16 - Change the Reset switch from NMI (12) the default to full CPU reset (23)
- JP17 - Selects CPU High speed when in High speed mode
  - Note : 1&2 are bridged by default and select 3.55 Mhz when in high speed mode
  - Note : 2&3 select 5.32 Mhz as the high speed mode. If bridging cut 1&2 first
- JP18 - Short pin to set CPU speed to Normal 1.77Mhz, or removed for high speed.
  - This can be routed to a switch, which could use a small capacitor to avoid bounce
- JP19 - Provide +5V power to external monitor via DIN connector. Cut to disable this
- JP20 - Used to support video output via RCA socket. Must be bridged to enable RCA
- JP21, JP27 - (REQUIRED) - Configures the type and Page of the main ROM. See silkscreen on the PCB
  - Note : JP21 controls Pin 21, and JP27 controls Pin 27 of the ROM socket
  - Note : Shorting Pin 1&2 = Logic 1 , while shorting Pin 2&3 = Logic 0
- JP30 - Allows EEPROM programming (support) by allowing WR signal to be routed to Pin 27
  - Note : Default of 12 disables Writes to EEPROM, deferring to setting on JP27
  - Note : Shorting 23 (cutting 12) enables Writes to EEPROM, ignoring setting on JP27
  - Note : This requires software to perform the programming.
- SW10 - SW13 - (REQUIRED) - Configures the Character generator ROM
  - Note : See silkscreen for details of this.
  - Note : Switched On = Logic 1, Switched Off = Logic 0
- RV2 - configures the signal level (volume) sent to the audio amplifier
- RV4 - horizontal position of video image
- RV5 - vertical position of video image

## Optional Headers

The following optional headers Pins are provided, you can choose to install or not install as required
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
  - Including U3 (SN75452), and U25 (LM3900)
  - Do not insert the CPU, ROMs, character generator, and RAMs for now.
- Use an oscilloscope test for a 1.77 Mhz Clock Signal on Pin 6 of the Z-80 CPU Socket
  - If not found then need to trace back to main oscillator
- Connect a CRT (preferable) monitor, you should see a video raster.
- Insert video generation chips
  - Static video RAM chip.
  - Insert character generator ROM.
- Ensure SW10 is configured for the chip type, and character set.
- When powered on you should see random but recognisable characters.
- With Power disconnected, Insert the main computer chips
  - Insert Z-80 CPU chip
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

## Usage Notes

### FreHD

Consider building the separate [FreHD board](/frehd/README.md) for use with this board.

### Expansion Interface

When connecting the Expansion interface (EI) its internal RAM needs to be disabled.
Noting: It is not good enough to remove the RAM chips themselves, as regardless of the
presence of RAM, the EI buffers the output of RAM back to main databus.

There are 2 approaches

Remove (de-solder) the 74LS244 buffer chips Z29, and Z31. This completely isolates the RAM
from the databus and is easily reversible by installing "socketed" chips. This makes it easier
to change going forward.

Disable the buffers from outputting back to the bus. There are 2 options that I can suggest
but without access to an expansion interface I am not sure which is easier;
* Cut trace leading out of Z28 Pin 6, and bridge Pin 19 of either Z29, or Z31 to Pin 20 (vcc)
* Cut trace leading into Z28 Pin 5, (or out of Z32 Pin 2) and bridge Z28 Pin 5 to Pin 7 (gnd)

There are probably other ways to achieve the same thing.
* The first approach requires more work, but simple to change on the fly.
* The second approach requires less overall work, but is harder to revert
