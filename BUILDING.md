
# Builders Guide

For V1 please see the [Builders Guide V1](/BUILDING-V1.md)

## Provided Files

The files provided in this project are primarily:

- The Schematics in PDF Format [Schematics PDF Format](/pcb/TRS-80-MP-SchematicsV2.pdf)
- Gerber files for manufacture [Gerbers ZIP](/pcb/TRS-80-MP_GerberV2.zip)
- Bill of Materials [BOM CSV Format](/pcb/TRS-80-MP-BillOfMatV2.csv)
- Also see the [Parts Guide](PARTS_GUIDE.md) for further advice on part usage

And the following
- A few compatible font have been provided in this project see [Fonts](/fonts/README.md)
- Customisable L2 ROM Images can be found here [TRS-80 Model 1 L2 Rom](https://github.com/kiwisincebirth/TRS-80)

## Assembly Order

Typically, solder components in order of the lowest profile to the tallest components.
- All Solder Jumpers should be (re-)configured as appropriate, 
  as easier to cut default traces if needed first, before installing other components
- All resistors, these can be installed in any direction
- Diodes, fitting CR5-CR8, and then CR4 last
- Ceramic capacitors with specifiv values - C3, C13, C17, C18, C43, C48, C50, C57, C60
- Decoupling (100nf) ceramic Capacitors, these are all remaining capacitors.
- Install any IC sockets you want, don't insert IC's at this point. 
  As a minimum you should be for CPU/RAM/ROM, but advisable to install for all.
- Resistor Packs, RN1, RN2
- Jumper Switch pack, SW10
- Crystal Y1
- Jumper J18 - Should be shorted for normal CPU frequency
- Jumper JP21, JP27 - Set the ROM Chip Type
- Jumper J15, J16, J17, J20, J21 are optional only solder if needed
- Cassette Relay K1
- Transistors Q1, Q2
- Power barrel Jack J11
- RV2 Trim resistor
- U4/U5 audio amplifier module
- Electrolytic Capacitors C19, C70, C101
- Install remaining Electrolytic Capacitors. Make sure the orientation is correct.
- Cassette DIN Socket J3
- Video Output J2 or J12. If soldering DIN socket don't solder (remove) centre pin
- Large Switches, noting solder either SW1 or S1, and SW2 or S2
- Keyboard header CN3, on front (or  rear) of the PCB.

## Patches

The following patches should be noted for the board. These were discovered after initial PCB manufacture, and affect
the boards design, and or the silkscreen.
- nothing known at this time.

## Configuration

Configuration is provided by several jumper options
- JP6 - (REQUIRED) - Used to configure video output to either 50Hz or 60Hz.
- JP10 - Configure how character generator selects its page number (LSB), switch vs software. 
  - Note : 1&2 are bridged by default, using SW13 to select the LSB char generator page
  - Note : Setting 2&3 enable software selection using (Port FF Bit 7), ignoring SW13. 
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
- JP21, JP27 - Configures the type and Page of the main ROM. See silkscreen on the PCB
  - Note : JP21 controls Pin 21, and JP27 controls Pin 27 of the ROM socket
  - Note : Shorting Pin 1&2 = Logic 1 , while shorting Pin 2&3 = Logic 0
- JP30 - Allows EEPROM programming (support) by allowing WR signal to be routed to Pin 27
  - Note : Default of 12 disables Writes to EEPROM, deferring to setting on JP27 
  - Note : Shorting 23 (cutting 12) enables Writes to EEPROM, ignoring setting on JP27
  - Note : This requires software to perform the programming.
- SW10 - SW13 Configures the Character generator ROM
  - Note : See silkscreen for details of this.
  - Note : The switch polarity is reversed Switched On = Logic 0, Switched Off = Logic 1
- RV2 - configures the signal level (volume) sent to the audio amplifier
- RV4 - horizontal position of video image
- RV5 - vertical position of video image

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
    - Static video RAM (U9) .
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

