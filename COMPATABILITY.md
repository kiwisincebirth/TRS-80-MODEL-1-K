# Compatible Components and Devices

## Parts Usage

### Crystal

Following Quartz Crystal's have been tested
* 10.6000 Mhz
* 10.7000 Mhz

### ROM's
Apart from the recommended AT28C256, the following ROM's have been tested
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

### Cassette Interface

CLOAD and CSAVE have NOT yet been tested.

Audio output (sound) has been tested and works.

### CPU Speed 

Double Speed (CPU speedup) is known to work. Note higher clock speeds require
components that can handle the extra speed. An original Z-80 was rated at 2Mhz
and may not work at higher speeds.

### Video Output

Both NTSC (60Hz), and PAL (50Hz) have been tested and are known to work.

## Expansion Devices

The following are devices confirmed to work with the Model 1 K

### FreHd (External)

An external FreHD plugged into edge connector appears to work. 
Tested and known working configurations include:
* FreHD connected via 40/0 pin hard drive adapter
* FreHD connected via Quinnerface
* FreHD connected via Expansion Interface (NOT TESTED)

Not Specifically relating to the Model 1K but more generally the following tips
* For the 40/50 Pin adapter there is a Jumper JP1, this should NOT be shorted as prevents computer boot.
* The SPAM chip should be removed from the Quinnerface, as it conflicts with the internal 48KB RAM

### FreHd (Internal)

The [FreHD](./frehd/README.md) internal board (part of this project)
has been built and tested, and has one known issue

Since an internal FreHD is powered from the main computer it won't typically
have enough time to boot before the main computer (CPU) trys to access it
via an auto boot ROM. The computer will need a hard reset after FreHD has fully booted.
Hard reset requires a patched ROM, that forces a hard reset when reset button is pushed.

### MIRE / MISE

Works with some minor issues.
