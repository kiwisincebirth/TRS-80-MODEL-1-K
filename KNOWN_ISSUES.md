# Known Issues

The following known issues were an the specific board versions. Note: If indicated the issues may also exist
in prior versions. Typically these issues are addressed in future versions. See the [Changelog](./CHANGELOG.md)
for the actual changes made.

## V1b

I have found an issue on the silkscreen for Character Generator Dip Switch settings SW10-13 which affects
this and all prior versions. Firstly the silkscreen label for SW13 is completely misaligned with the 
DIP switch's themselves. 

Also the silkscreen for the settings themselves should read.

```
Char   SW10  SW11  SW12  SW13
28256   OFF   A14   A13   A12
27512   A14   A15   A13   A12
27256   A14   OFF   A13   A12
27128   OFF   OFF   A13   A12
OFF = Logic 1 ; ON = Logic 0
```

Previously it (*Incorrectly*) stated.

```
Char   SW10  SW11  SW12  SW13
28256  OFF   A14   A13   A12
27512  A14   A15   A13   A12 
27256  A14   ON    A13   A12
27128  OFF   ON    A13   A12
```

Noting SW11 for 27256, 27128 show `ON` incorrectly. This is partly
confusion because an ON => Logic 0, while OFF => Logic 1

## V1

The following minor should be noted for the board. These were discovered after initial PCB manufacture, and affect
the boards design, and or the silkscreen. NOTE: The following have be fixed in V1a (and latter) of the board.

- The main power connector (J11) GND pins use thermal reliefs, ideally they shouldn't. To provide better 
  GND connection a wire (from the GND pin) should be connected to the GND pins of the video connector.
- Z50 should be a SN7404N, not a 74LS04 as labelled. Z50 acts as an amplifier and requires an unbuffered part.
- Z6, and Z65 should be a SN74**LS**92, not a 74HCT92 as labelled. The 7492 was never produced in HCT variant
- Z32 can be a 74**HCT**00 just like other digital logic. The specific use of 74**C**00 is not required.
- C51 (decoupling capacitor) duplicates C79 and is not required. While it does no harm it we be removed in future. 

And the following issues were fixed from V1b and latter revisions
- Thermal reliefs are missing on power rails connecting to most IC's. When soldering you need to use a higher
  temperature soldering iron for these pins, and ensure the soldering iron comes into direct contact with the pcb pad
- The footprints for C19 (capacitor), Q1, Q2 (transistors) is not modern, the legs of the components 
  will need to be bent outwards and the component mounted higher to fit correctly 
- The footprint for CR4 diode is too small making the diode harder to fit, you will need to bend the legs
  exactly to fit, and possibly sanding the legs may make it easier to mount
