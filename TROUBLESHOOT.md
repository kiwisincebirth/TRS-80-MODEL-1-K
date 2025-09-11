# Troubleshooting

## General

### General Assembly
* Ensure all Components are correctly soldered.
    * It is not uncommon to find components installed without all pins soldered.
    * Look for any dry solder joints.
      * Note: in initial builds there was lack of thermal reliefs on power pins, so check these specifically
    * Look for any missing components.
    * Look for any solder bridges between pins/pads, test with continuity checker.
* Ensure all socketed IC's are correctly installed
    * Ensure no bent pins on inserted IC's
    * IC's are inserted with the correct orientation
    * IC's are inserted in the correct sockets
    * Possibly remove and reseat if in doubt

### Power Supply
* Check the input power supply.
    * Check voltage (5V) and polarity (centre positive) of power supply.
    * Check the power supply is well regulated, with  little noise.
    * Potentially try a different power supply to see if this works.
* Ensure Power is getting to all components.
    * Check power is being transferred through the barrel jack.
    * Check the main switch is switching power on and off.
    * Check voltages across power pins of all IC's are showing 5V.
    * Alternately check for continuity of VCC, and GND pins to known pins.
* Check electrolytic capacitors are installed with correct polarity.

### Configuration
* Check solder jumpers are bridged correctly
    * For 3 pin jumpers, ensure no continuity between soldered and un-soldered pads.
* Check all required jumpers are correctly installed.

## Specific Guides

### Main Clock
* Ensure main crystal oscillator is generating 10.6445 Mhz
    * If not consider installing patch capacitor

### No Video Signal

If not seeing a stable video raster then, need to diagnose the Timing chain
* Assuming the main crystal is working, working forward
* Ensure hdrv, vdrv are outputting correct frequencies
* Ensure hsync and vsync should be be outputting correct frequencies
* then check for a sync pulse, which is mixed from hsync and vsync
* finally check the video mixing circuit to output composite video

A component in this timing chain is proably the issue and needs to be replaced.

### Video Corruption

If seeing an all white raster or random but stable pixels than potentially
* the character generator ROM may not programmed correctly
* or the DIP switches may not be set correctly for the rom type, page number

If see a repeating (same) character across the entire screen then
* potentially the VRAM is not working correctly.

This is a much bigger topic, the above is not complete. Please follow other TRS-80 troubleshooting guides.  
Ensure you can see a stable image, of random ascii/graphic characters before continuing.

# Advanced

The following shouldn't really be needed, it is with the assumption that a component has failed
which is unlikely in a new build. Note: the following is also incomplete

### CPU Operation
IF the computer is not booting to a known good state based on the ROM installed, then
need to diagnose the operation of the computer itself, typically CPU, ROM, RAM, and some
supporting circuitry are required

If available try a different CPU / RAM / ROM chips

This is a much bigger topic, the below is not complete. Please follow other
Z80 TRS-80 troubleshooting guides.

#### CPU
If cannot see any activity on CPU need to checks its input signals
* Power 5V, and GND is being supplied
* RESET - should pulse low at power on then stay high
* CLOCK - should by 1.7 Mhz
* NMI - should stay high
* INT - should stay high
* ADDRESS LINES - should show activity
* DATA LINES - should show activity

#### ROM
Remove the ROM chip entirely, if everything else is functioning you should see video fill up
with 2 characters repeated, the 2 characters may vary (typically `@9`) depending on char set.

Need to Check the input to the ROM

#### RAM
Installing a Diagnostic ROM can be used to test the function of RAM
