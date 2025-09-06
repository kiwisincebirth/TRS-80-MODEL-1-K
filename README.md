# TRS-80-MODEL-1-K

TRS-80 Model 1k - Hardware Replacement Main board - Evolution (Rev K)

## Introduction

This project is an upgraded / evolved TRS-80 Model 1 main board replacement. It was designed to provide a reliable, 
compact, and modern replacement, removing some limitations of the original 1970's product, 
while still remaining faithful to the original technology (i.e. no emulation) 

![MainboardFrontBuiltK1](/images/IMG_8736.jpeg)

For more images [See Here](./images/README.md)

### What this is:
- Drop in (mostly) replacement main board for existing TRS-80 Model 1
- Modernised using larger density (memory) components to reduce component count
- Onboard some common features, that required a piggyback board's or piggyback IC's
- Provides some level of additional internal expansion, or ability to evolve the board itself.
- Remains faithful to the use of traditional thru-hole parts, and discrete logic IC's

### What this isn't:
- Is not compatible with 32Kb external RAM expansion, external RAM will need to be disabled.
- Is not compatible with Model 1 power supply. It requires a fully regulated 5V DC power supply.
- Is not a faithful recreation of the original Model 1, other projects exist for this.

### Features at a Glance
- CPU double speed (3.56 Mhz), configurable by jumper or external switch.
- System ROM's have been replaced with standard 32 pin EPROM (27xxx) or EEPROM (28xxx).
- Larger ROM's allow multiple paged ROM images selectable by Jumper.
- ROM can be configured to occupy the empty memory region (12-14kb) above the main ROM.
- A full 48Kb of RAM is provided by a single modern SRAM chip.
- Video character generation is provided by standard 32 pin 27xxx EPROM's or 28xxx EEPROM's
- Video character generator provides full 6x12 pixel matrix (Gendon3 compatible) descenders.
- Multiple character sets can be defined, the character set chosen is by dip switches.
- The Video sync has been upgraded with improved stability, and 50Hz PAL support.
- Video Output is via traditional DIN, or optional RCA socket.
- An internal 40 pin header is provided for plug in expansion cards
- A [FreHD board](./frehd/README.md) has been developed primarily for internal expansion.
- Power and Reset switches can be either traditional or modern components. 
- The cassette input has minor improvements in the A/D design.
- All internal power regulation circuitry has been removed, now externally provided.
- Overall modernisation, including full GND planes, decoupling capacitors, silkscreen. 
- A prototyping area is provided on the board, for user provided enhancements.

See the separate [Features](./FEATURES.md) for the overall design and full list of features

## Building

See the separate [Builders Guide](/BUILDING.md) for complete technical documentation

Included with this project are:
- All required materials and guides to order and assemble this project.
- A [FreHD board](/frehd/README.md) that can be connected directly to the mainboard, and installed internally.
- A selection of [Font Files](/fonts/README.md) for use with this project.
- A selection of [ROM Images](/roms/README.md) for use with this project.

## Status / Future

See the separate [Status and Future](/STATUS.md) which provides a mini update blog for this project

## Credits

- The Board Folk Ver 1.1 Japanese board without which this project would not be possible.
    - https://github.com/Board-Folk/TRS80IJP
- Glens stuff TRS-80 Model 1 clone, of which some inspiration was taken.
    - https://www.glensstuff.com/trs80/trs80.htm
- VCF Forums for some help and guidance
    - https://forum.vcfed.org/index.php?threads/trs-80-model-1-board-design.1251905/
- The Tandy Discord Channel for feedback, help and support
    - MSly, Marcel Erz, Maboytim, Tuc
