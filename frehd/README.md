# FreHD for the Model 1

## Introduction

This is a project to provide a FreHD that directly connects to the TRS-80 Model 1 40 pin expansion port.
It was designed to be functionally compatible using primarily all the same parts, 
and also software compatible, as it uses he same PIC and GAL firmware

It was designed to work with the Model 1 either
* internally within the Model 1k via it's 40 pin internal expansion port.
* or attached externally to any Model 1 via appropriate 40 pin ribbon cable.

Attaching it to a Model 1's expansion port, means there is no need for a 40/50 pin adapter.

The physical layout of the board while different still has the 
power and IO connection is on one side, and SD card and LED's on the other.
Mounting holes and some pinouts are different.

![3D Render](/frehd/images/Board3dRender.png)

### Improvements

The problematic 5V to 3.3V level shifter (Q1), and the voltage dividers implemented in resistors,
has been replaced with a small PCB module that provides level shifting and mounts in a 12 pin
DIP package. This package provides the appropriate transistors and resistors in SMT components.

The original design drove the WAIT bus signal (to high) preventing other peripherals to co-exist 
on the bus. A modification to the design allows for Open Collector output on the WAIT signal to resolve this.
To provide open collector a revised (different) version of the GAL firmware must be programmed, and Jumper J1 
on the board switched from 1-2 (default),to 2-3.

General improvements include, an optional onboard PCB reset pushbutton, full GND and Power planes, 
as well as more decoupling capacitors located (where possible) closer to chip VCC's

### Modifications

The J4 power connector may not have same pinout as modern (v1.3) FreHD. 

The J1 header for external LED's and Reset, has the pinout adjusted for direct compatibility with
microchip programmer ICSP pinout.

The IOREQ signal provided to GAL has been removed and the GAL input tied to GND. 
It was determined that this signal was not required, as it duplicated RW/WR 
signals which were also present. This also mean that additional components
found on the Model 1 Hard disk adapter (transistors/resistors) that generated
this signal were also not required.

The RS232 capability has been omitted from the board.

See comments in the schematic for other modifications made.

## Building

### Files

The [pcb](./pcb) directory contains
* [PDF Schematics](./pcb/FreHD-SchematicV1.1.pdf), 
* Gerber files, and Bill of Materials.

### Parts

Generally all parts (excepting PCB) are generally the same as the original excepting the following changes:

* [U8 - Sparkfun Quad Logic Level Converter Bidirectional](https://www.sparkfun.com/sparkfun-logic-level-converter-bi-directional.html)
* [BT1 - Memory Protection Devices BS7 Batter Holder](https://www.memoryprotectiondevices.com/datasheets/BS-7/BS-7.pdf)

Also note the BOM does not have exact manufacturer part numbers, the part numbers were taken 
from the original FreHD designs. The following is a partial list of modern part numbers,
others will have to be determined. These are some other notable major components:

* [J2 - Hirose DM1AA-SF-PEJ82 - SD Card Socket](https://au.mouser.com/ProductDetail/Hirose-Connector/DM1AA-SF-PEJ82?qs=q%252B4FLHukgWBHaRKRr0HV%252Bw%3D%3D)
* [U1 - PIC18F4620-IP - Microcontroller](https://au.mouser.com/ProductDetail/Microchip-Technology/PIC18F4620-I-P?qs=sX%2FisSQq3c4Cme3RX0st5A%3D%3D)
* [U2 - Microchip Technology ATF16V8B-15PU - PLC](https://au.mouser.com/ProductDetail/Microchip-Technology/ATF16V8B-15PU?qs=2mdvTlUeTfCsdBIzx6v3gA%3D%3D) or Lattace GAL16V8
* [U3 - 74LS245]
* [U4 - TI LP2950CZ-3.3/LFT3 - 3.3 voltage regulator](https://www.digikey.com.au/en/products/detail/texas-instruments/LP2950CZ-3-3-LFT3/3640733) or TS2950
* [U6 - 74LS595]
* [U7 - DS1307+ - Realtime clock](https://www.digikey.com.au/en/products/detail/analog-devices-inc-maxim-integrated/DS1307/956883)
* [Y1 - 10Mhz - Quartz Crystal]
* [Y2 - 32.7kHz - Quartz Crystal - 12.5pf](https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-327-6-13X/6821661)

### Assembly

The first step is probably to decide if you want the open collector WAIT signal,
requiring a reprogrammed GAL, if so you need to Cut JP1 1,2 and solder 2 to 3

Note: Unless you need this it may be safer to stick with the default, as may cause 
confusion latter, if the GAL needs replacing, have to ensure the modified firmware is programmed.

The next step is to solder the SMD SD card, followed by the through hole components.

As a minimum sockets need to be installed for PIC and GAL, so they can be reprogrammed.
IC sockets are preferred on other components e.g. RTC, and 7400 series logic so they 
can be replaced, but it is not strictly essential.

U8 (The 12 pin level shifter) should be soldered to the board,
using small short pin headers. It should **NOT** be installed in a socket.

J3 The 40 pin IO connector should be either 
* For internal connection - A Female socket soldered to the reverse side of the board
* For external connection - Male header pins soldered to the front of the board

The 40 pin connection carries data signals, and gold contact pins should be chosen as a preference.
If using internally it is best to solder the female header's (J3, J6) (reverse side of the board)
in situ. i.e. placing the female header's onto the Model 1k board's header and soldering the
board to the socket, allowing for a small clearance with components on the main board.

Solder components typically in size and height order, typically from the lowest profile to highest, 
and from smallest to largest. The only exception is the small crystal oscillator, 
it is sensitive to damage, maybe consider soldering it latter.

### Optional Parts

If required you can choose to solder one of the following options.
The first option is typically the default. 

Power connection is via 1 of 2 header sockets.
* J6 - Designed for use with the modern TRS-80 Model 1k (evolution) internal expansion port.
  Providing VCC only, GND comes from he 40 pin IO connector
* J4 - Providing VCC and GND via similar header to the original board. For external power.

Dual sets of onboard LED's are provided, maximum of one of either:
* Populate - D1, D2, R13, R14 - for mounting on the rear on the PCB
* Populate - D11, D12, R33, R34 - for mounting on the front on the PCB
* External LED's via J1

Optional external Programming Header:
* J1 - for external PIC programming, OR external reset and LED's

Optional reset for the PIC:
* SW1 - for onboard reset pushbutton

## Programming

The PIC must be programmed. See the separate [Programming PIC](PROGRAMING.md) guide.

The GAL must be programmed. There are 2 versions
* The original GAL [FreHD GAL](https://github.com/veco/FreHDv1/tree/main/hw/gal)
* The modified GAL [Open Collector GAL](https://github.com/maboytim/FreHDv1/tree/main/hw/gal-oc)

## Troubleshooting

See the separate [Trouble Shooting Guide](TROUBLE.md)

## Additional

Additional Images can be found here [Images](./images/README.md)

## Resources

The use of the FreHD is not well documented, see [Resources](./RESOURCES.md)

## Credits

The original designer without which this project would not be possible

maboytim - for support in coming up with open collector design on the WAIT bus signal,
and for investigating the use of IOREQ signal and its use in the GAL logic.
