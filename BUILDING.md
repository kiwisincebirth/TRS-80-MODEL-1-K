
# Builders Guide

## Provided Files

The files provided in this project are primarily:

- The Schematics in PDF Format [Schematics PDF Format](/pcb/TRS-80-MP-SchematicsV2.pdf)
- Gerber files for manufacture [Gerbers ZIP](/pcb/TRS-80-MP_Gerberv2.zip)
- Bill of Materials [BOM CSV Format](/pcb/TRS-80-MP-BillOfMatV2.csv)

also see the parts guide [Parts Guide](PARTS_GUIDE.md)

## Assembly Order

Typically, solder components in order of the lowest profile to the tallest components.
- Solder jumpers for Video Frequency (JP6, JP7, JP8, JP10) and Rom Memory Size (J13, J14)
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
- JP6, JP7, JP8, and JP10 - Used to configure video output to either 50Hz or 60Hz.
- JP13, JP14 - Size of the main system ROM as either 12KB (standard), 13KB, or 14KB
  - Note : 1&2 are bridged by default and need to be cut for any change.
  - Note : Using a 14KB ROM size will prevent the use of Model 1 floppy controller or printer port which occupy
    memory in the 0x37E0 - 0x37FF range. If using a 14kb ROM the 0x37E0 - 0x37EF memory address should probably
    return 0xFF so (if installed) a Level 2 ROM will not think a floppy controller is attached.
- JP15 - Enable output of HDRV on Video DIN socket for RGBtoHDMI support (from 1.0a)
- JP16 - Change the Reset switch from NMI (12) to full CPU reset (23)
- JP19 - Provide +5V power to external monitor via DIN connector. Cut to disable 
- JP21, JP27 - Configures the type and Page of the main ROM. 
  - Note : JP21 controls Pin 21, and JP27 controls Pin 27
  - Note : Shorting Pin 1&2 = Logic 1 , while shorting Pin 2&3 = Logic 0
- SW10 - SW13 Configures the Character generator ROM
  - Note : See silkscreen for details of this.
  - Note : The switch polarity is reversed Switched On = Logic 0, Switched Off = Logic 1
- J18 - Short pin to set CPU speed to Normal 1.77Mhz, or removed for 2x speed.
  - This can be routed to a switch, which could use a small capacitor to avoid bounce
- RV2 - configures the signal level (volume) sent to the audio amplifier

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

