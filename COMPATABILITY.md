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
* Legacy Power Switch (untested at present)
* Modern Reset Switch
* Legacy Reset Switch (untested at present)

## Functional Tests

### Video Output

The following video output have been tested and work as expected.
* NTSC (60Hz) - using a 10.6 Mhz crystal, both CRT and Modern device
* PAL (50Hz) - using a 10.7 Mhz crystal, only tested with Modern device

### CPU Speed 

Double Speed (CPU speedup) is known to work. Note higher clock speeds require
components that can handle the extra speed. An original Z-80 was rated at 2Mhz
and may not work at higher speeds.

### Cassette Interface

Cassette LOAD and SAVE have been tested (10.6Mhz crystal) and are working as expected. This is regardless
of the clock speedup setting since the CPU is automatically slowed on cassette access.

Audio output (sound) has been tested and works.

### Internal IO

The Internal IO header has been tested with external devices connected via 40 pin ribbon cable
to the internal IO 40 pin header. This requires cable with a female header attached to one end. 

## Expansion Devices

The following are devices confirmed to work with the Model 1 K

### FreHd (External)

An external FreHD plugged into edge connector appears to work. 
Tested and known working configurations include:
* FreHD connected via 40 to 50 pin hard drive adapter
* FreHD connected via Quinnerface
* FreHD connected via Expansion Interface (NOT TESTED)

Not Specifically relating to the Model 1K but more generally the following tips
* For the 40/50 Pin adapter there is a Jumper JP1, this should NOT be shorted as prevents computer boot.
* The SPAM chip should be removed from the Quinnerface, as it conflicts with the internal 48KB RAM

### FreHd (Internal)

The [FreHD](./frehd/README.md) internal board (part of this project)
has been built and tested, and has one known issue

Since an internal FreHD is powered from the main computer it may not
have enough time to boot before the main computer (CPU) trys to access it
via an auto boot ROM. The computer will need a hard reset after FreHD has fully booted.
Hard reset requires a patched ROM, that forces a hard reset when reset button is pushed.

This issue may be fixed with a different version of the autoboot rom that adds a small delay
during startup.

### MIRE / MISE

Works with some minor issues.

### TRS-IO

Unknown


