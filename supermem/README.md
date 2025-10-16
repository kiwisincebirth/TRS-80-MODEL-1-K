# SuperMem 512KB

## Introduction

The SuperMem board is an addition to the Model 1k that provides 512KB of Banked RAM
compatible with the SuperMem 512 for the Model 1

This is implemented as a small board that replaces the 128 Kbyte SRAM chip on the M1k 
main board, and contains the 512KB SRAM and the necessary bank control logic.

There are 2 board revisions, one for V1 and a second for V2. Each version is designed 
for each version to the M1k to fit around other existing components. Functionally they 
are the same.

A PLC (programmable logic chip) - GAL22V10 or equivalent is required and needs to be 
programmed with the provided firmware 

Three additional wires are required to be connected to signal's ( IN , OUT , SYSRES )
on the main board.

## Parts

The main components required:
* Lattace GAL22V10 or equivalent programmed with the provided firmware 
* AS6C4008-55PCN 4 Mbit - 512 Kbyte RAM chip
* 74HCT174 Latch
* 74HCT244 Buffer
* 100nf Capacitors (x4)
* Pin Headers for installing in socket on Main board
* IC sockets

## Assembly Options

There are 2 overall options for assembly. Each has its own advantages. 

### Socket the components

Socket the components onto the memory board, and Solder the memory board to the main board.

This means that the board can no longer be removed, but the chips can be replaced
if any issues arise. It the SuperMem functionality needed to be disabled
the GAL would need to be reprogrammed, or replaced with jumpers that provide 
constant signals to the upper address lines.

### Socket the board

Solder the components to the memory board, and Socket the memory board onto the main board. 

This makes it easy to reverse the modification, but the components on the board 
are harder to remove. If a compoent failed, then proably easier to build a new board.

Note the programmable GAL **Should Always** be installed in a socket.

## Board Assembly

First solder the pin headers to the underside of the board, ensuring correct alignment.
It is best to put the pin headers into a matching socket while soldering.

Trim the pin headers on the top of the board, to allow 512KB SRAM chip (or socket) 
to be installed flush with the board itself. It may help to trim the legs prior to soldering
to achive a flush surface

Next solder the IC's to the top of the board, using sockets only if you intend 
to solder this board to the main board. Note the GAL chip should *NOT* be soldered.

Solder the decoupling capacitors to the board.

Clean the board with isopropyl alcohol removing any flux residue.

Solder three wires to the underside of the board allowing suitable length to solder to 
the appropriate pins on the main board

Install chips into the memory board into the sockets, if not already soldered

If soldering this board to the main board, then it is **Important** to check that **ALL** soldering
on the underside of the board has been performed, once soldered to the main board it is difficult 
to correct.

## Installation

Potentially you may need to remove the decoupling capacitor from the RAM socket on the main board
to ensure the memory board has sufficient clearance. Removing this capacitor should be fine
as each component on the memory board has its own capacitor.

Install the memory board to the main board, into socket, or solder as appropriate.

Route the three wires to correct signals and solder these. On V2 board there are three test points
located close to the RAM chip specifically for this purpose.

## Testing

Use the SuperMem test program or run the basic program.

```
MEM SIZE ? 32000

5 POKE 32767,42
10 FOR N = 0 TO 15:OUT 67,N:POKE -1,N:NEXT N 
20 FOR N = 0 TO 15:OUT 67,N:PRINT PEEK(-1);:NEXT X 
25 PRINT PEEK(32767)
```



