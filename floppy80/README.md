# Floppy 80 for the Model 1

## Introduction

This is a project to provide a Floppy 80 that connects to the TRS-80 Model 1 
via a standard 40 pin header compatible with standard IDC cable.
It was designed to be functionally compatible using primarily all the same parts, 
and also software compatible, as it uses he same firmware.

The floppy 80 (for M1) project is located here
[MichaelM4 Floppy80-M1](https://github.com/MichaelM4/Floppy80-M1)

It was designed to work with the Model 1 either
* internally within the Model 1k via it's 40 pin internal expansion port.
* or attached externally to any Model 1 via appropriate 40 pin ribbon cable.

![MainboardFront](./images/IMG_0150.jpeg)

See comments in the schematic for modifications made to the original design.

## Building

### Files

The [pcb](./pcb) directory contains
* [PDF Schematics](./pcb/Floppy80_schematic_v1.pdf), 
* Gerber files for JLCPCB or PCBWAY
* Kicad Files

### Parts

All parts (excepting PCB) are generally the same as the original excepting the following changes:

* [J3 - Hirose DM1AA-SF-PEJ82 - SD Card Socket](https://au.mouser.com/ProductDetail/Hirose-Connector/DM1AA-SF-PEJ82?qs=q%252B4FLHukgWBHaRKRr0HV%252Bw%3D%3D)

### Assembly

The board is dual sided, and has SMD components care must be taken

The order of assembly, while not definitive, following is advice 
* U1, U3, U4, U5 - Logic IC's on the rear of the board
* SD Card Socket on the front of the board
* Small SMD components on the rear of the board
* The PI Pico on the rear of the board
* Small SMD components on the front of the board

Lastly solder through hole components:
* For internal connection - components go on the front of the board, same as SD card socket
* For external connection - components go on the reae of the board, same as logic IC's

J2 The 40 pin IO connector should be either
* For internal connection - A Female socket soldered to the reverse side of the board
* For external connection - Male header pins soldered to the front of the board

The 40 pin connection carries data signals, and gold contact pins should be chosen as a preference.
If using internally it is best to solder the female header's (J1, J2) (reverse side of the board)
in situ. i.e. placing the female header's onto the Model 1k board's header and soldering the
board to the socket, allowing for a small clearance with components on the main board.

### Optional Parts

Optional Power connection
* J1 - Designed for use with the modern TRS-80 Model 1k (evolution) internal expansion port.
  Providing VCC only, GND comes from he 40 pin IO connector
* If mounting externally power is typically provided via the USB port on the Pico

Optional Resistors
* R6 and R8 should be considered optional, they are in the original design
however in my opinion they afre not needed, as the computer itself has 4k7 pullup resistors

## Programming

The Pi must be programmed ... todo

## SD Card Setup

An SD card must be setup ... todo

## Additional

Additional images can be found here [Images](./images)

## Credits

The floppy 80 (for M1) project is located here
[MichaelM4 Floppy80-M1](https://github.com/MichaelM4/Floppy80-M1)
