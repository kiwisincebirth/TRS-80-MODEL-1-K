
# Builders Guide

## Provided Files

The files provided in this project are primarily:

- The Schematics in PDF Format [Schematics PDF Format](/pcb/TRS-80-MP-SchematicsV1b.pdf)
- Gerber files for manufacture [JLCPCB ZIP](/pcb/TRS-80-MP_JLCPCBV1b.zip) and [PCBWAY ZIP](/pcb/TRS-80-MP_PCBWayV1b.zip)
- Bill of Materials [BOM CSV Format](/pcb/TRS-80-MP-BillOfMatV1b.csv)
- A visual BOM is also available [VISUAL BOM](/pcb/TRS-80-MP-BomVisualV1b.html)
- Also see the [Parts Guide](PARTS_GUIDE.md) for further advice on part usage
- Also see the [Ordering](ORDERING.MD) guide for how to place a component order

And the following
- A few compatible font have been provided in this project see [Fonts](/fonts/README.md)
- Customisable L2 ROM Images can be found here [TRS-80 Model 1 L2 Rom](https://github.com/kiwisincebirth/TRS-80)

## Assembly Order

Before starting need to look at the solder jumpers on the board.
- JP6, JP7, JP8, JP10 on the board is Required be configured as appropriate for either
  50Hz (PAL) or 60Hz (NTSC) video. Just need to solder a bridge on Pins 1&2 or 2&3
- Other solder jumpers on the board can be changed at any time and have
  reasonable default connections. If changing you will probably need to cut existing connection

Most components are labeled on the PCB, as you install each component you should check its value
against what is in the BOM, and cross it off. An interactive BOM is provided to aid in this process

Typically, solder components in order of the lowest profile to the tallest components.
- All resistors, these can be installed in any direction
- Diodes, fitting CR5-CR8, and then CR4 last
- Ceramic capacitors with specifiv values - C3, C13, C17, C18, C43, C48, C50, C57, C60
- Decoupling (100nf) ceramic Capacitors, these are all remaining capacitors.
- Install any IC sockets you want, don't insert IC's at this point. 
  As a minimum you should be for CPU/RAM/ROM, but advisable to install for all.
- Resistor Packs, RN1, RN2
- Jumper Switch pack, SW10
- Crystal Y1 - I used a 10.7 Mhz crystal without any issues
- Jumper J18 - Should be shorted for normal CPU frequency
- Jumper JP21, JP27 - Set the ROM Chip Type
- Jumper J15, J16, J17, J20, J21 are optional only solder if needed
- Cassette Relay K1
- Transistors Q1, Q2
- Power barrel Jack J11
- Electrolytic Capacitors C19, C70, C101
- Install remaining Electrolytic Capacitors. Make sure the orientation is correct.
- Cassette DIN Socket J3
- Video Output J2 or J12. If soldering DIN socket don't solder (remove) centre pin
- Large Switches, noting solder either SW1 or S1, and SW2 or S2
- Keyboard header CN3, on front (or  rear) of the PCB.

## Patches

The following patches should be noted for the board. These were discovered after initial PCB manufacture, and affect
the boards design, and or the silkscreen. NOTE: The following have be fixed in V1a of the board.
- To get the main crystal oscillator to function a 100pf capacitor was installed connecting pins 5 to 7 of Z50

Additionally, please see the [Known Issues](./KNOWN_ISSUES.md) which describe issues with the board design itself,
that should also be addressed during build.

## Configuration

Configuration is provided by several jumper options
- JP6, JP7, JP8, and JP10 - Used to configure video output to either 50Hz or 60Hz.
- JP13, JP14 - Size of the main system ROM as either 12KB (standard), 13KB, or 14KB
  - Note : 1&2 are bridged by default and need to be cut for any change.
  - Note : Using a 14KB ROM size will prevent the use of Model 1 floppy controller or printer port which occupy
    memory in the 0x37E0 - 0x37FF range. If using a 14kb ROM the 0x37E0 - 0x37EF memory address should probably
    return 0xFF so (if installed) a Level 2 ROM will not think a floppy controller is attached.
- JP21, JP27 - Configures the type and Page of the main ROM. 
  - Note : JP21 controls Pin 21, and JP27 controls Pin 27
  - Note : Shorting Pin 1&2 = Logic 1 , while shorting Pin 2&3 = Logic 0
- SW10 - SW13 Configures the Character generator ROM
  - Note : See silkscreen for details of this.
  - Note : The switch polarity is reversed Switched On = Logic 0, Switched Off = Logic 1
- J18 - Short pin to set CPU speed to Normal 1.77Mhz, or removed for 2x speed.
  - This can be routed to a switch, which could use a small capacitor to avoid bounce

## Testing

For each of the step (when inserting components) ensure power is turned off and disconnected. 
You will need to power on to perform necessary tests

Follow these steps
- Don't install any socketed IC's yet
- Connect a regulated 5V supply
- Using multimeter test for +5V on J17
- With power turned On
- Test for +5V on a few IC sockets Pin 14 or 16 around the board.
- with Power disconnected Insert all simple socketed logic chips
    - Including all 74xx series logic
    - Including Z3 (SN75452), and Z25 (LM3900)
    - Do not insert the CPU, ROMs, character generator, and RAMs for now.
- Powered on, use an oscilloscope test for a 1.77 Mhz Clock Signal on Pin 6 of the Z-80 CPU Socket
- Connect a CRT (preferable) monitor, you should see a video raster.
- Insert Video generation chips
    - Static video RAM (Z9, Z10) - 2114.
    - Insert character generator (U37). Ensure SW10 is configured for the the chip type, and character set.
- When powered on you should see random but recognisable characters.
- Insert CPU, RAM, and ROM
    - Insert CPU (Z48) Z-80
    - Insert RAM (U15)
    - Install ROM. Preferably use the latest 1.3 version. Ensure JP21, JP27 are configured for the chip type
- You should see a prompt showing "MEM SIZE?" (if it is the normal system ROM). You should see random characters being input, this is normal
- Install the keyboard with the IDC cable (if you installed a header).
- Now, you should be able to use the system.

Additional Testing to consider:
- Load and save a program to cassette tape
- Run a Hello World program: 10 PRINT "Hello World!" (Return) 20 GOTO 10 (Return) RUN (Return). 
  You should run this for some time. You can stop with the BREAK key.
- 32 character mode PRINT CHR$(xx) or right arrow and clear on the keyboard
- Another program to try ; 10 PRINT MEM;:IF MEM >100 GOSUB 10 ELSE RUN

