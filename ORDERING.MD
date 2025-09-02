
# Ordering Guide

## Ordering PCB 

Either PCBWAY or JLCPCB can be used, and specific output files have been generated for each supplier.

For JLCPCB The following notes apply when ordering
* tbd

For PCBWAY the following notes apply when ordering
* tbd

## Ordering Parts

### Digikey

The Bill of Materials has been constructed primarily from parts provided by DigiKey.
If ordering from other parts suppliers then alternatives may need to be substituted

## Bill of Materials

The BOM contains the following important fields
* Reference - Used to identify component in Schematic / PCB
* MF - The name of the manufacturer of the part
* MP - The manufacturers part number
* Qty - Quantity

### Hard to Find

The following components are Included in the BOM but are considered obsolete/hard to find and may 
need to be sourced separately as mainstream suppliers dont necessarily hold them in stock.
See the Parts Guide for further info on suitable replacements and where they may be ordered:
* The main Z80 CPU
* Video Memory Chip(s)
* 10.6445 Mhz Crystal Oscillator

### Component Choice

The board offers several choices on several connectors between a primary modern 
vs optional traditional part.  Noting the BOM includes the primary component, 
so if you intend to use the optional component you need to source it separately, 
and remove the primary component from the BOM prior to ordering

* Modern Power Switch (SW1) -> vs optional traditional locking pushbutton (S1) 
* Modern Reset Button (SW2) -> vs optional traditional pushbutton (S2)
* Video Output 5 Pin DIN" Connector (2) -> vs optional RCA connector (J12)

### Optional Components

IC Sockets are not included in the BOM. While optional, they are highly recommended for all IC's, 
and should be considered mandatory for all large scale components, e.g. CPU,
RAM (including Video RAM), and ROM (including Character Generator). 

IC sockets typically come in two types, traditional with square/flat holes, and the newer rounded
machine pins. In my experience I have found the traditional square sockets to be more forgiving
and are probably better for the larger IC's.

Several optional Pin Headers have not been included in the BOM as
they are not necessary in a standard configuration, and can be added at a latter date

For V2 of the board an optional onboard Audio Amplifier Module and Speaker can be 
installed. This requires specific sourcing and mounting and thus excluded from the BOM.
See Parts Guide for more information

## Manufacturing

### Unmounted Components

A few components have been included in the BOM but will not be installed by a manufacturing process
as it is expected these components be installed manually possibly by the end user.

* Keyboard Pin Header (CN3) - Should be mounted according to your preference.
* Large Power Capacitor (C101) - Mount Horizontally to reduce height
* 10.6445 Mhz Crystal Oscillator (Y1) - Must be mounted horizontally for height clearance
* C61 Patch - Mount only if necessary to make main oscillator run.
* 40 Pin Internal IO Pin Header (J20, J21) - Should be mounted when and only IF needed.
* Power LED (V2 Only) - May not be wanted, nor is it really necessary
* Pin Jumpers - For shorting config Pins are included but not mounted

## Additional Notes

### Alternate Main Clock

The main board (V1-RevB and latter) supports two types of main Clock
* A standard quartz crystal with 7404 circuit (the traditional design)
* A modern DIP-14 Can oscillator (discussed below)

A DIP-14 Can oscillator is a self-contained metal package (similar to normal quarts crystal) 
that comes in a DIP-14 pinout, but only has 4 pins exposed.
* Pin 1 Enable
* Pin 7 Ground
* Pin 8 Main Clock TTL Level Output
* Pin 14 VCC

This component outputs a TTL level clock which is directly usable, without the need for any 
external components. The existing circuit (and the 7404 pinout) has been designed so
the Oscillator can be installed in place of the 7404.
This means all the supporting circuitry (including the quartz crystal) can be removed.

A programmable oscillator is available from DigiKey, ("ECS-P145") and can exactly match
the required frequency, improving reliability, the part itself has not been tested.
Owing to height restrictions it is unlikely the oscillator could be socketed.

* https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-P145-AN/502317
* https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-P145-BX/965972
* https://www.ecsxtal.com/store/pdf/ecs-p143x-p145x.pdf

Also the following, (more a curiosity)
* https://github.com/schlae/ClockInACan
