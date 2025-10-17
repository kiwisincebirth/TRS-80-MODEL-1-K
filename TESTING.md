
# Testing Guide

This guide details the initial testing steps required after assembly is complete

## Prior to Testing

Before testing you should have completed the assembly, but not inserted any socketed chips.
Please review the board to ensure all components are installed and soldered.

You will need a regulated power supply that provides 5V. The connector is a center positive
barrel jack, and is quite common to find this connection in 12V power supplies, however these are not
compatible. The board performs no power regulation so a good quality power source is required.

**WARNING!!** - Connecting a 12V Power supply will probably **damage several components on the board**.
Please **test the power supply** for correct voltage and polarity **before connecting**.

## Testing Procedure

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
    - Including Z/U3 - SN75452, and Z/U25 - LM3900
    - Do not insert the CPU, ROMs, character generator, and RAMs for now.
- Use an oscilloscope test for a 1.77 Mhz Clock Signal on Pin 6 of the Z-80 CPU Socket
    - If not found then need to trace back to main oscillator
    - For V1 board consider installing C61 (Patch) to make main oscillator run.
- Connect a CRT (preferable) monitor, you should see a video raster.
- Calibrate the Video [Sync Duration](./CONFIG.md#sync-duration-calibration). Version 2 Only!
- Insert video generation chips
    - Static video RAM chip or chips(s).
    - Insert character generator ROM.
- Ensure SW10 is configured for the chip type, and character set.
- When powered on you should see random but recognisable characters.
- With Power disconnected, Insert the main Z80 processor chip.
- When powered on you should see the display fill up with repeating `@9`characters
    - This indicates the CPU is functioning and executing code.
- With Power disconnected, Insert the main system RAM, and ROM chip's
- Ensure JP21, JP27 are configured for the ROM chip type you are using
- When powered on, you should see a prompt showing "MEM SIZE?" (if it is the normal system ROM).
    - You may see random characters being input, this is expected since keyboard is not connected
- Install the keyboard with the IDC cable (if you installed a header).
- Now, you should be able to use the system.

## Additional Testing

Additional Testing to consider:
- Load and save a program to cassette tape
- Run a Hello World program: 10 PRINT "Hello World!" (Return) 20 GOTO 10 (Return) RUN (Return).
  You should run this for some time. You can stop with the BREAK key.
- 32 character mode PRINT CHR$(xx) or right arrow and clear on the keyboard
- Another program to try ; 10 PRINT MEM;:IF MEM >100 GOSUB 10 ELSE RUN
