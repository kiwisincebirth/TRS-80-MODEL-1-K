# Parts Guide

For V1 please see the [Parts Guide V1](/PARTS_GUIDE-V1.md)

## Specific Parts Used

###  Crystal Oscillator (10.6445 Mhz)

https://www.mutant-caterpillar.co.uk/shop/product_info.php?products_id=5174

https://www.ebay.com/itm/195727646631\

Mouser Stock 10.695Mhz crystals (as well as 10.7Mhz)

https://www.mouser.com/ProductDetail/IQD/LFXTAL003560Bulk?qs=e4%2FAndAAwgLcW9WGosgF2g%3D%3D

or 10.7 mhZ (next closest) can come from China

https://www.aliexpress.com/item/1005006183714474.html
https://www.aliexpress.com/item/1005003752108473.html
https://www.alibaba.com/product-detail/QZ-new-high-quality-10-7M_1601237726803.html

The main board supports a standard crystal oscillator
in the DIP-14 Full Can form factor. This can be installed in place of the 74HCU04 (U50).
This allows custom oscillators to be used instead of the 74HCU04 circuit. e.g.

https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-P145-AN/502317
or
https://github.com/schlae/ClockInACan
or
https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-P145-BX/965972
https://www.ecsxtal.com/store/pdf/ecs-p143x-p145x.pdf

### Main System ROM

Supports 27128, 27256, 27512 EPROM, or 28256 EEPROM - 28 pin devices

I would recommend using a Microchip Technology AT28C256-15PU
This gives 2 16KB ROM banks and is electrically erasable.

https://octopart.com/at28c256-15pu-microchip-77758240

### Character Generator ROM

Same as main system ROM

### Main System RAM

Alliance Memory AS6C1008-55PCN 

https://octopart.com/search?q=AS6C1008-55PCN&currency=USD&specs=0
https://www.digikey.com.au/en/products/detail/alliance-memory-inc/AS6C1008-55PCN/4234576

### Video Memory

1 KB Dual Port SRAM. There are 2 options:

IDT7130LA55P 

https://octopart.com/search?q=IDT7130LA55P
https://www.renesas.com/en/products/memory-logic/multi-port-memory/asynchronous-dual-port-rams/7130-1k-x-8-dual-port-ram
https://www.renesas.com/en/document/dst/713040-datasheet

CY7C130-55PC (older part number)

https://octopart.com/search?q=CY7C130-55PC
https://www.rocelec.com/part/01t4w00000POumrAAD-CY7C13055PC
https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/380/CY7C130%2C131%28A%29.pdf
https://www.silicon-ark.co.uk/datasheets/CY7C131-datasheet-cypress.pdf

Do Not Use IDT7140, CY7C140, CY7C141, these are Slave devices and NOT compatible

### Amplifier Module

A small 6 pin module based on either LTK5128, or XPT8871 chipset.

Googling these chip IDS you will find the modules themselves. There are three variants
which differ in pcb colour/size, pinout, and main capacitor size. 
They are commonly available from online chinese stores, ebay or amazon.

There are 2 pin outs supported, one of these offers a Mute function, which
is activated when the cassette motor is on.

For more information about the chip itself. Noting datasheets are in chinese
https://components101.com/ics/XPT8871-audio-amplifier-ic-pinout-datasheet-circuit

### Joystick Port DB9 Cable

Requires a straight thru DB9 cable. See for information on the cable: 

https://www.scantips.com/serial-db9.html

### Cassette Relay

Omron G5V-1

https://omronfs.omron.com/en_US/ecb/products/pdf/en-g5v_1.pdf

### RCA Video Connector

https://neurochrome.com/products/rca-connectors

can be obtained easily on Ali express.

### Power Connector

https://core-electronics.com.au/dc-barrel-power-jack-connector.html

can be obtained fairly easily from multiple sources, these usually come in either 2.1 or 2.5mm 
you need to choose the best one based on the power brick you intend to use.

### Power Switch

https://www.digikey.com.au/en/products/detail/e-switch/100AWDP1T1B4M6QE/1803008

https://configured-product-images.s3.amazonaws.com/Datasheets/100A.pdf

https://www.altronics.com.au/p/s1360-salecom-dpdt-horizontal-action-pcb-mount-mini-toggle-switch/

https://www.salecom.com/en/product/t8021.html

### Reset Switch

https://www.digikey.com.au/en/products/detail/e-switch/800SP8B6M6RE/502075

https://configured-product-images.s3.amazonaws.com/Datasheets/800.pdf

https://www.altronics.com.au/p/s1495-salecom-spdt-mom.-90-deg.-pcb-sub-mini-pushbutton-switch/#/

https://www.salecom.com/en/product/es-22a.html

### DIN Connector

The footprint for this type of connector seems fairly standardised

https://www.digikey.com.au/en/products/detail/same-sky-formerly-cui-devices/SDS-50J/97033
https://www.digikey.com.au/en/products/detail/switchcraft-inc/57PC5F/275385

https://www.switchcraft.com/assets/1/24/57PC5F_CD.pdf?5023

https://www.aliexpress.com/item/1005006314983600.html

### Discrete Components

Some additional Notes about some components used:
- Except for R37 (a 1/2 watt resistor) all resistors are 1/4 watt, preferably metal film, 5% tolerance or better.
- All ceramic capacitors are 100V tolerance 10% unless otherwise specified
- C105, C106, C107, C108 used in the timing logic of Video Sync generation should utilise high stability parts.
- R21 and R22 are also used in the video sync, so high tolerance values should be used
  or use a multimeter to find a resistor that is identical to what is specified.
- Electrolytic capacitors should be rated to 16 volts, less is not advisable, more is not really required.

### Trim Resistors

Trim Resistors are Bourns multi turn vertical, with inline pin. These are identifiable by the marking "3296" on the side

https://www.bourns.com/pdfs/3296.pdf

### CMOS Part Usage

This project has been built primarily with CMOS (TTL compatible) 74HCTxxx components, 
with the following notable exclusions
- U50 should be a SN7404HCU, it acts as an amplifier and requires an unbuffered part.
- Z6, and Z65 should be a SN74LS92, the x92 was never produced in HCT variant
