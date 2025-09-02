# Parts Guide

## Hard to Find Parts

### Z80 CPU

The part is no longer in production, and needs to obtained seperatly. Preference if for:
* CMOS variant, but this is not critical since older NMOS TTL is compatible
* 6MHz since it is possible to overclock the computer to 5.3Mhz

###  Crystal Oscillator (10.6445 Mhz)

An exact replacement part is available, for a high cost
* https://www.mutant-caterpillar.co.uk/shop/product_info.php?products_id=5174
* https://www.ebay.com/itm/195727646631\

Mouser Stock 10.695Mhz crystals (as well as 10.7Mhz)
* https://www.mouser.com/ProductDetail/IQD/LFXTAL003560Bulk?qs=e4%2FAndAAwgLcW9WGosgF2g%3D%3D

10.7 mhZ (next closest) can come from China
* https://www.aliexpress.com/item/1005006183714474.html
* https://www.aliexpress.com/item/1005003752108473.html
* https://www.alibaba.com/product-detail/QZ-new-high-quality-10-7M_1601237726803.html

### Video Memory

1k x 4 bit SRAM - TMS2114L-15 or uPD2114LC-5 or equivalent

Several Providers of this component have been identified
* https://www.rocelec.com/part/01t4w00000PQTxNAAX-TMS2114L15NL
* https://www.silicon-ark.co.uk/mm2114-15l-static-ram-by-national-semiconductor?search=2114
* https://www.scribblygum.com.au/index.php?route=product/product&product_id=229
* https://www.arcadepartsandrepair.com/store/integrated-circuits/ram-memory/2114-ram/
* https://twistywristarcade.com/ram/43-2114-ram.html

Datasheet's
* https://www.lcsc.com/datasheet/C20918461.pdf
* https://www.silicon-ark.co.uk/datasheets/uPD2114l-datasheet-nec.pdf

## Alternate Part Usage

The design of the board allows for several components to be chosen as either Traditional
or a more modern component, this is typically the external connectors and switches

### Video Connector

The RCA video connector can be obtained easily on Ali express, just search for "RCA PCB"
The datasheet for the part is provided here.
* https://neurochrome.com/products/rca-connectors

The traditional (DIN) video connector is described below

### Power Switch

Modern Power Switch
* https://www.digikey.com.au/en/products/detail/e-switch/100AWDP1T1B4M6QE/1803008
* https://configured-product-images.s3.amazonaws.com/Datasheets/100A.pdf
* https://www.altronics.com.au/p/s1360-salecom-dpdt-horizontal-action-pcb-mount-mini-toggle-switch/
* https://www.salecom.com/en/product/t8021.html

Traditional Power Switch can be sourced from

### Reset Switch

The modern Reset Pushbutton
* https://www.digikey.com.au/en/products/detail/e-switch/800SP8B6M6RE/502075
* https://configured-product-images.s3.amazonaws.com/Datasheets/800.pdf
* https://www.altronics.com.au/p/s1495-salecom-spdt-mom.-90-deg.-pcb-sub-mini-pushbutton-switch/#/
* https://www.salecom.com/en/product/es-22a.html

### Alternate Main Clock

The main board (V1-RevB and latter) supports two types of main Clock
* A standard quartz crystal with 7404 circuit
* A modern DIP-14 self-contained oscillator

The advantage of the self-contained oscillator is that it replaces the
entire close circuit with a single module which is installed in place of the 7404
and all the supporting circuitry can be removed. Digikey provide a programmable
module which can re-produce the clock frequency to a high accuracy
* https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-P145-AN/502317
* https://www.digikey.com.au/en/products/detail/ecs-inc/ECS-P145-BX/965972
* https://www.ecsxtal.com/store/pdf/ecs-p143x-p145x.pdf

Also the following, (more a curiosity)
* https://github.com/schlae/ClockInACan

## Parts Reference

### System and Character ROM

Supports 27128, 27256, 27512 EPROM, or 28256 EEPROM - 28 pin devices. I would recommend
using a Microchip Technology AT28C256-15PU. This gives 2 16KB ROM banks and is
electrically erasable.
* https://octopart.com/at28c256-15pu-microchip-77758240
* https://www.digikey.com.au/en/products/detail/microchip-technology/AT28C256-15PU/1008506

### Main System RAM

Main System RAM is provided by a 128KB SRAM Chip - Alliance Memory AS6C1008-55PCN
* https://octopart.com/search?q=AS6C1008-55PCN
* https://www.digikey.com.au/en/products/detail/alliance-memory-inc/AS6C1008-55PCN/4234576

### Cassette Relay

The cassette Relay is an Omron "G5V-1 DC5"
* https://omronfs.omron.com/en_US/ecb/products/pdf/en-g5v_1.pdf
* https://www.digikey.com.au/en/products/detail/omron-electronics-inc-emc-div/G5V-1-DC5/87831

### Power Connector

It can be obtained fairly easily from multiple sources, these usually come in either 2.1 or 2.5mm
you need to choose the best one based on the power brick you intend to use.
However, 2.1mm seems to be the more common one in use.
* https://core-electronics.com.au/dc-barrel-power-jack-connector.html

### DIN Connector

The footprint for this type of connector seems fairly standardised and freely available
* https://www.digikey.com.au/en/products/detail/same-sky-formerly-cui-devices/SDS-50J/97033
* https://www.digikey.com.au/en/products/detail/switchcraft-inc/57PC5F/275385
* https://www.switchcraft.com/assets/1/24/57PC5F_CD.pdf?5023
* https://www.aliexpress.com/item/1005006314983600.html

## General Notes

### Discrete Components

Some additional Notes about some components used:
- Except for R37 (a 1/2 watt resistor) all resistors are 1/4 watt, preferably metal film, 5% tolerance or better.
- All ceramic capacitors are 100V tolerance 10% unless otherwise specified
- C105, C106, C107, C108 used in the timing logic of Video Sync generation should utilise high stability parts.
- R21 and R22 are also used in the video sync, so high tolerance values should be used
  or use a multimeter to find a resistor that is identical to what is specified.
- Electrolytic capacitors should be rated to 16 volts, less is not advisable, more is not really required.

### CMOS Part Usage

This project has been built primarily with CMOS (TTL compatible) 74HCTxxx components, 
with the following notable exclusions
- Z50 should be a SN7404N, it acts as an amplifier and requires an unbuffered part.
- Z6, and Z65 should be a 74LS92, the x92 was never produced in HCT variant
- The Video RAM chips 2114 are obsolete and only available in TTL
