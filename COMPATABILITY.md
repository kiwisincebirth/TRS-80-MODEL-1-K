# Compatible Components and Devices

## Parts Usage

### Quartz Crystal

The following Quartz Crystal's have been tested
* 10.6000 Mhz
* 10.7000 Mhz

### ROM's
Apart from the recommended AT28C256, the following ROM's have been tested
* 27C512
* 27C256
* 27128

### Video Memory
The following video memory chips have been tested and are known to work.
* uPD2114LC (NEC)

### IO Connectors

Following connectors have specifically been tested
* DIN Video Connector
* RCA Video Connector
* Modern Power Switch
* Legacy Power Switch
* Modern Reset Switch
* Legacy Reset Switch

## Functional Tests

### Video Output

The following video output have been tested and work as expected.
* NTSC (60Hz) - using a 10.6 Mhz crystal, both CRT and Modern device
* NTSC (60Hz) - using a 10.7 Mhz crystal, both CRT and Modern device
* PAL (50Hz) - using a 10.7 Mhz crystal, only tested with Modern device

### CPU Speed 

Double Speed (CPU speedup) is known to work. Note higher clock speeds require
components that can handle the extra speed. An original Z-80 was rated at 2Mhz
and may not work at higher speeds.

### Cassette Interface

Cassette LOAD and SAVE have been tested with either 10.6Mhz, and 10.7Mhz crystal's and are working as expected. 
This is regardless of the clock speedup setting since the CPU is automatically slowed on cassette access.

Audio output (sound) has been tested and works.

### Internal IO

The Internal IO header has been tested with external devices connected via 40 pin ribbon cable
to the internal IO 40 pin header. This requires a cable with a female header attached to one end. 

## Expansion Devices

The following are devices confirmed to work with the Model 1 K

### Model 1 Expansion Interface

When connecting the Expansion interface (EI) its internal RAM needs to be disabled.
Noting: It is not good enough to remove the RAM chips themselves, as regardless of the
presence of RAM, the EI buffers the output of RAM back to main databus.

#### Newer Revised Expansion Interface

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

#### Original Expansion Interface

In the original Expansion Interface, and referring to method 1 above, the two 74LS367 buffer 
chips that need to be removed (desoldered and socketed) are Z19, Z21, and optionally Z22.

Referring to Option 2 (above) Z20 Pin 2, or 3 ; or Z37 Pin 13 or 14 seem like the easiest places
to intercept the signal but this option is left undefined at this time.

### FreHd (External)

An external FreHD plugged into edge connector appears to work. 
Tested and known working configurations include:
* FreHD connected via 40 to 50 pin hard drive adapter
* FreHD connected via Quinnerface
* FreHD connected via Expansion Interface (NOT TESTED)

Not Specifically relating to the Model 1K but more generally the following tips
* For the 40/50 Pin adapter there is a Jumper JP1, this should NOT be shorted as prevents computer boot.
* The SPAM chip should be removed from the Quinnerface, as it conflicts with the internal 48KB RAM

#### Some Issues

The FreHD appears to provide parasitic power back to the Model 1K (assumed via WAIT signal)
This causes a 15-second delay before power can successfully be reapplied (with FreHD powered)

Resolutions
* Power the FreHD from the internal power on the Model 1K
* Update the FreHD with Open Collector WAIT signal.
* Reduce the size of the large filtering capacitor C101 to 220uF - 470uF
* Install a bleed resistor 100 ohms 1/2 watt across the Model 1K main power rail

### FreHd (Internal)

The [FreHD](./frehd/README.md) internal board (part of this project)
has been built and tested, and has one known issue

Since an internal FreHD is powered from the main computer it may not
have enough time to boot before the main computer (CPU) trys to access it.
The computer will need a hard reset after FreHD has fully booted.
If no expansion interface (floppy controller) is connected, 
a patched ROM may be required to force hard reset from the user reset button.

This issue may be fixed with a different version of the autoboot ROM
that adds a small delay during startup.

### MIRE / MISE

Is known to have some incompatibility. The following was investigated by MSly (discord channel):

The MIRE seems to work fine - except for the reset button, which locks up the system.

The MIRE with MISE connected boots up, but the reset button returns to Mem Size instead of a reboot.

The MISE is incompatible with the Model 1k. I am having issues with LDOS not returning from a standard DIR command.
It doesn't seem to be able to recognize the last drive - just hangs requiring a power cycle on both the MISE and M1K.
This behavior is not seen on a Rev G.

### TRS-IO

Not Tested


