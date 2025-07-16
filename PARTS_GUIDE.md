# Parts Guide

## Specific Parts Used

###  Crystal Oscillator (10.6445 Mhz)

https://www.mutant-caterpillar.co.uk/shop/product_info.php?products_id=5174

https://www.ebay.com/itm/195727646631\

Mouser Stock 10.695Mhz crystals (as well as 10.7Mhz)

https://www.mouser.com/ProductDetail/IQD/LFXTAL003560Bulk?qs=e4%2FAndAAwgLcW9WGosgF2g%3D%3D

or 10.7 mhZ (next closest) can come from China

https://www.aliexpress.com/item/1005006183714474.html

https://www.aliexpress.com/item/1005003752108473.html

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

uDP2114LC or equivalent

### Cassette Relay

Omron G5V-1

https://omronfs.omron.com/en_US/ecb/products/pdf/en-g5v_1.pdf

### RCA Video Connector

https://neurochrome.com/products/rca-connectors

can be obtained easily on Ali express.

### Power Connector

https://core-electronics.com.au/dc-barrel-power-jack-connector.html

can be obtained fairly easily from multiple sources, these usualy come in either 2.1 or 2.5mm you need to chhose the best 
one based on the power brick you intend to use.

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

### CMOS Part Usage

This project has been built primarily with TTL compatible CMOS (74HCTxxx) components, 
with the following notable exclusions
- Z50 should be a 7404N, it acts as an amplifier and requires an unbuffered part.
- Z65 should be a 74LS92, the 7492 is only readily available in LS series
