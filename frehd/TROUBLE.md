
# Troubleshooting

## Basic Things to Check

From a Hardware Perspective
* Check for Missing Components
* Soldering is complete, no missing Pins
* Soldering is correct, no dry solder joints
* Check Orientation of components

Voltages
* Check for 5V supplied to the PIC
* Check for 3.3V supplied, check HV Pin of BOB module

SD Card
* Is formatted using FAT
* Has a FREHD.ROM file in root directory
* Try a different SD Card

Firmware versions need to be hecked for the latest.
* PIC - 2.17 seems to be the latest
* GAL - This hasn't changed alot but worth reading its contents are valid
* Level 2 Basic ROM - Suggest getting it from my
[TRS-80-ROMS](https://github.com/kiwisincebirth/TRS-80-ROMS/releases) github page 

CPU Speed
* For testing purposes ensure the CPU speedup is disabled (jumper installed)

## Startup

At Startup the Green LED should flash once. This indicates the PIC firmware has stared.
If you don't get a flash, then
* Is VCC getting to PIC, Pins ???
* Ensure a clock signal is getting to the PIC
* Try a known good PIC, or alternate PIC
* Ensure the LEDs are soldered in correct orientation.
* Try reprogramming the PIC

### Diagnosis from Basic

TODO - Needs summary from below forum posting's

### Forum Articles

And I found some third party utilities

[VCF Forums Help with a DIY FreHD](https://forum.vcfed.org/index.php?threads/help-with-a-diy-frehd.1247210)
[Google Groups FreHD issues](https://groups.io/g/TRS-80/topic/89558376)
