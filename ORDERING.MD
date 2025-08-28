
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
* Z80 CPU (Z48)
* Video Memory Chip(s)
* 10.6445 Mhz Crystal Oscillator (Y1)

### Component Choice

The board offers several choices on several connectors between a primary modern 
vs optional traditional part.  Noting the BOM includes the primary component, 
so if you intend to use the optional component you need to source it separately, 
and remove the primary component from the BOM prior to ordering

* Modern Power Switch (SW1) -> vs optional traditional locking pushbutton (S1) 
* Modern Reset Button (SW2) -> vs optional traditional pushbutton (S2)
* Video Output 5 Pin DIN" Connector (2) -> vs optional RCA connector (J12)
* Crystal Oscillator -> See Notes Additional below. 

### Optional Components

IC Sockets are not included in the BOM. While optional they are highly recommended for all IC's, 
and should be considered mandatory for all large scale components, e.g. CPU,
RAM (including Video RAM), and ROM (including Character Generator). 

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

### Crystal Oscillator

2 options are possible - 74HCU04 (default approach in BOM) with a quart crystal, 
or using a Dip 14 CAN oscillator.
Noting the 74HCU04 pinout was designed to be pin (1,7,8,14) compatible with a CAN oscillator 
and thus can be replaced directly, then all discrete components (including crystal) removed.

A programmable oscillator is available from DigiKey, ("ECS-P145") and can exactly match 
the expected frequency, this should improve reliability, the part itself has not been tested.
Owing to height restrictions it is unlikely the oscillator could be socketed.
