# Known Issues

The following known issues were found on the specific board versions. Note: the issues probably also exist
in prior versions. Typically, these issues are addressed in future versions. See the [Changelog](./CHANGELOG.md)
for the actual changes made.

## V2a

### Clock Speed (Transition)

MSly (discord channel) has uncovered an issue when clock speed is transitioned from Fast <-> Slow,
Sometimes the computer will lock up.

Diagnosing the issue it appears that the circuit that controls the transition from one clock frequency to
another is not well-timed, and can occur just after the current clock has transitioned, and switch to
the new clock then causes another level transition. This resulting is a very short duration clock pulse,
in the order of 30ns. Depending on the CPU used this can be out of tolerance causing the issue.

The resolution is either to use a fast CPU, which is more tolerant, or simply disable high speed.

# Version 1

## V1c

### Power Capacitor

MSly (discord channel) has uncovered an issue with C101 (2200uF), which takes about 5 seconds to discharge
after power is removed. If power is reapplied before the capacitor has had significant time to 
discharge then the computer won't boot. This is primarily observed as the video displaying showing the
last screen contents (maybe dependent on the SRAM used) when power was disconnected.

With externally powered devices (still powered on), there is a possibility of parasitic power increasing this time.
With a FreHD it was observed it took 15 seconds for the power to be sufficiently drained to allow normal startup.

The Resolution is to replace C101 which a much smaller capacitor in the range, 220uF - 470uF. Additionally, 
installing a bleed resistor 100 ohms 1/2 watt across the main power rail, will improve the situation
This bleed resistor will draw a consistent 1/4 watt of power.

### Clock Speed (Transition)

MSly (discord channel) has uncovered an issue when clock speed is transitioned from Fast <-> Slow,
Sometimes the computer will lock up. 

Diagnosing the issue it appears that the circuit that controls the transition from one clock frequency to 
another is not well-timed, and can occur just after the current clock has transitioned, and switch to 
the new clock then causes another level transition. This resulting is a very short duration clock pulse,
in the order of 30ns. Depending on the CPU used this can be out of tolerance causing the issue.

The resolution is either to use a fast CPU, which is more tolerant, or simply disable high speed.

### Also

There is an issue with the Legacy Power switch, there is (ony slightly) not enough spacing between pins. 
This means that getting all six pin rows installed is problematic. A workaround is to remove/cut the 
first row of pins (closest to the pushbutton), this should allow the remaining 5 rows of pins to be installed.
Noting: That this row is NOT electrically required. Credit to @GaryK - discord for reporting this.

Another issue is that when installing SuperMem board there is no easy way to route the 3 signal wires.
The only alternative is to probably drill a hole, and feed wires through the board. There is space
just above and to the right of the RAM chip that is suitable for a hole, as it has just GND planes.

The silkscreen doesn't show what components can be removed when installing the alternate main clock.

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

## V1a

the following issues were discovered and fixed from V1b and latter revisions

- Thermal reliefs are missing on power rails connecting to most IC's. When soldering you need to use a higher
  temperature soldering iron. Also ensure the soldering iron comes into direct contact with the pcb pad
- The footprints for C19 (capacitor), Q1, Q2 (transistors) is not modern, the legs of the components 
  will need to be bent outwards and the component mounted higher to fit correctly 
- The footprint for CR4 diode is too small making the diode harder to fit, you will need to bend the legs
  exactly to fit, and possibly sanding the legs may make it easier to mount

## V1

The following minor should be noted for the board. These were discovered after initial PCB manufacture, and affect
the boards design, and or the silkscreen. NOTE: The following have be fixed in V1a (and latter) of the board.

- The main power connector (J11) GND pins use thermal reliefs, ideally they shouldn't. To provide better 
  GND connection a wire (from the GND pin) should be connected to the GND pins of the video connector.
- Z50 should be a SN7404N, not a 74LS04 as labelled. Z50 acts as an amplifier and requires an unbuffered part.
- Z6, and Z65 should be a SN74**LS**92, not a 74HCT92 as labelled. The 7492 was never produced in HCT variant
- Z32 can be a 74**HCT**00 just like other digital logic. The specific use of 74**C**00 is not required.
- C51 (decoupling capacitor) duplicates C79 and is not required. While it does no harm it we be removed in future. 


