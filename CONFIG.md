# Configuration

## Jumpers

Configuration is provided by several jumper options

### Version 2 Jumpers

The following applies to **Version 2** of the board

Configuration is provided by several jumper options:
- JP6 - (REQUIRED) - Used to configure video output to either 50Hz or 60Hz.
- JP10 - Configure how character generator selects its page number (LSB), switch vs software.
  - Note : 1&2 are bridged by default, using SW13 to select the LSB char generator page
  - Note : Setting 2&3 enable software selection using (Port FF Bit 7), ignoring SW13.
- JP12 - Configure the use of an all RAM machine, replacing the use of ROM. This is provided
  as an experimental feature, a boostrap process will be needed to initialise the computer
  - Note : If shorting this the ROM chip itself should be removed.
  - Note : If shorting this JP14 (1&2) cannot be bridged, instead (2&3) must be used.
- JP13, JP14 - Configure either RAM or ROM to be mapped into the 12-13kb and 13-14kb address space
  - Note : Using the 13-14kb address space will prevent the use of Floppy disk
    or printer which occupy memory in the 0x37E0 - 0x37FF range.
  - Note : If using the 13-14kb address space unmodified Level 2 ROM may cause issues.
    I have included modified ROMs to deal with these issues.
- JP15 - Enable output of HDRV on Video DIN socket for RGBtoHDMI support
  - Note : Only bridge this if installing DIN connector, RCA connector can't use it
- JP16 - Change the Reset switch from NMI (12) the default to full CPU reset (23)
- JP17 - Selects CPU High speed when in High speed mode
  - Note : 1&2 are bridged by default and select 3.55 Mhz when in high speed mode
  - Note : 2&3 select 5.32 Mhz as the high speed mode. If bridging cut 1&2 first
- JP18 - Short pin to set CPU speed to Normal 1.77Mhz, or removed for high speed.
  - This can be routed to a switch, which could use a small capacitor to avoid bounce
- JP19 - Provide +5V power to external monitor via DIN connector. Cut to disable this
- JP20 - Used to support video output via RCA socket. Must be bridged to enable RCA.
- JP21, JP27 - (REQUIRED) - Configures the type and Page of the main ROM. 
  - Note : See Section Below [System ROM](#system-rom)
- JP30 - Allows EEPROM programming (support) by allowing WR signal to be routed to Pin 27.
  This is provided as an experimental feature.
  - Note : Default of 12 disables Writes to EEPROM, deferring to setting on JP27
  - Note : Shorting 23 (cutting 12) enables Writes to EEPROM, ignoring setting on JP27
  - Note : This requires software to perform the programming.
- SW10 - SW13 - (REQUIRED) - Configures the Character generator ROM
  - Note : See Section Below [Font Rom V2](#font-rom-v2)
- RV2 - configures the signal level (volume) sent to the audio amplifier.
- RV4 - horizontal position of video image.
- RV5 - vertical position of video image.

### Version 1 Jumpers

The following applies specifically to **Version 1** of the board

Configuration is provided by several jumper options
- JP6, JP7, JP8, and JP10 - (REQUIRED) - Used to configure video output to either 50Hz or 60Hz.
- JP13, JP14 - Size of the main system ROM as either 12KB (DEFAULT), 13KB, or 14KB
  - Note : 1&2 are bridged by default and need to be cut for any change.
  - Note : Using a 14KB ROM size will prevent the use of Model 1 floppy controller or printer port which occupy
    memory in the 0x37E0 - 0x37FF range. If using a 14kb ROM the 0x37E0 - 0x37EF memory address should probably
    return 0xFF so (if installed) a Level 2 ROM will not think a floppy controller is attached.
- JP21, JP27 - (REQUIRED) - Configures the type and Page of the main ROM.
  - Note : See Section Below [System ROM](#system-rom)
- SW10 - SW13 - (REQUIRED) - Configures the Character generator ROM
  - Note : See Section Below [Font Rom V1](#font-rom-v1)
- J18 - Short pin to set CPU speed to Normal 1.77Mhz, or removed for 2x speed.
  - This can be routed to a switch, which could use a small capacitor to avoid bounce

## Video Calibration

In Version 2 of the Model 1k the Video Sync Pulse generation is adjustable, and must be calibrated.
This should be done during initial testing after the board has been assembled

Calibration of the Horizontal and Vertical sync pulse delays (positions) is done
via Trim potentiometers RV4 and RV, and can be done at any time.

Calibration of the Horizontal and Vertical sync pulse durations is done by R16 & R18.
These are parallel (to R17 R19) and are used to trim/calibrate the sync pulse durations.

Ideally R16 and R18 should be chosen in the testing stage when accurate measurements
can be taken and actual values chosen.

### Sync Duration Calibration

To accurately control the duration of the Horizontal and Vertical sync pulses an
oscilloscope is required to measure the actual sync pulse duration. The following
procedure can be followed:

During assembling do **NOT** install R16 and R18. Once assembled and powered on, 
h.sync and v.sync pulse can be calibrated independently:

This process can be done without other major components (e.g. CPU/RAM/ROM) being inserted,
but does require the main crystal oscillator to be fully functional.

- Connect an oscilloscope to test points h.sync (or v.sync) on the PCB.
- Place (hold) the default resistor in the trim resistor position and measure the pulse duration.
- If the duration is too long, try a smaller resistor (but not smaller than 2K ohms)
- You may need to test several resistors, to find a suitable value
- If duration is too short try a larger resistor, or omit entirely.

| Sync       | Duration | Test Point            | Trim Resistor | Default Value |
|------------|----------|-----------------------|---------------|---------------|
| Horizontal | 4.7 uS   | h.sync (or U50 pin 5) | R16           | 62K ohms      |
| Vertical   | 256 uS   | v.sync (or U51 pin 5) | R18           | 24K ohms      |

The default values of R16, and R18 can be used which will produce sync signals which
while may not be 100% accurate, should generally be within tolerance. The tolerance depends on the
accuracy to the other components used (specifically C6, and C8).

Once values for R16, and R18 have been found they can be solder to the board permanently

## Configuring ROM Paging

The following section applies to Character Font and System ROM's.

The system supports standard (E)EPROM from 128 KBit (16KB) to 512 KBit (64KB)

Depending on the ROM chosen and the use (Char Font/System) multiple pages can be used. 
The following table shows for each combination, the maximum number of pages
that can be programmed and the address bits used for the control of page selection

|                      | Char Font ROM | System ROM |
|----------------------|---------------|------------|
| **Base Image**       |               |            |
| Base Image Size      | 4 KB          | 16 KB (*1) |
| Address Lines Used   | A0 - A11      | A0 - A13   |
| **Available Pages**  |               |            |
| Max Pages (512 KBit) | 16            | 4          |
| Max Pages (256 KBit) | 8             | 2          |
| Max Pages (128 KBit) | 4             | 1          |
| **Page Addressing**  |               |            |
| Address Lines (512)  | A12 - A15     | A14 - A15  |
| Address Lines (256)  | A12 - A14     | A14        |
| Address Lines (128)  | A12 - A13     | n/a        |

**NOTE 1:** System ROM's require the use of 16 KB, i.e. to be exact power of 2, 
even though typically only the first 12 KB is actually usable by the CPU 

The mapping of the address line(s) is covered below.

### Char Font ROM

Since a character font ROM occupies 4 KB it uses A0-A11 
to address its data, leaving A12-A15 (depending on chip) for page control

#### Font Rom V1

**Warning** The silkscreen on the V1 PCB is incorrect. Only use the table below.

| PROM TYPE | SW10 | SW11 | SW12 | SW13 |
|-----------|------|------|------|------|
| 28256     | OFF  | A14  | A13  | A12  |
| 27512     | A14  | A15  | A13  | A12  |
| 27256     | A14  | OFF  | A13  | A12  |
| 27128     | OFF  | OFF  | A13  | A12  |

Notes:
- In V1 of the board DIP Switches were inverted in meaning i.e
  - Switched ON = Logic 0, and switched OFF = Logic 1
  - This was corrected in V2 and latter revisions.

#### Font Rom V2

| PROM TYPE | SW10 | SW11 | SW12 | SW13 |
|-----------|------|------|------|------|
| 28256     | ON   | A14  | A13  | A12  |
| 27512     | A14  | A15  | A13  | A12  |
| 27256     | A14  | ON   | A13  | A12  |
| 27128     | ON   | ON   | A13  | A12  |

Switched ON = Logic 1, Switched OFF = Logic 0

### System ROM

Since a System ROM occupies 16 KB (typically 12 KB used) it uses A0-A13
to address its data, leaving A14-A15 (depending on chip) for page control.

| PROM TYPE | JP21 | JP27 |
|-----------|------|------|
| 28256     | A14  | 12   |
| 27512     | A15  | A14  |
| 27256     | 12   | A14  |
| 27128     | 12   | 12   |

Notes:
- Bridging 1&2 Provides Logic Level 1
- Bridging 2&3 Provides Logic Level 0
- JP21 controls Pin 1, and JP27 Pin 27 of the IC

## Combining ROM Images

The following describes how to combine ROM images at the command line

### Padding System ROM's

When combining System ROM images they must be **padded to exactly
16,384 bytes in length**. There are two ways to do this.
* Append a 4 KB file to each ROM image before combining them into final image
* Simply reuse a 4 KB padding file in-between each image in a single copy command.

While not essential I suggest the padding is done with the `FFh` byte.
This leaves the (E)EPROM effectively un-programmed in this area.
Also (if enabled in future) extending the ROM into the 12KB - 14KB area,
`FFh` gives the maximum backward compatibility, with unoccupied memory.

### Windows

To append binary files from the Windows command line, the copy command with the /b switch is used. 
This switch designates the files as binary, ensuring that all characters, including special 
control characters, are copied as data without interpretation.

```copy /b file1.bin + file2.bin + file3.bin combined.bin```

This command concatenates file1.bin, file2.bin, and file3.bin into a new file named combined.bin.

### Linux / Mac

To append binary files from the command line on a Linux/Mac, you can use the cat command.
The cat command concatenates files and prints them to standard output. 

By redirecting the output you can effectively append one or more files into a new one.

To combine file1.bin, file2.bin, and file3.bin into a new file named combined.bin, 
use the `>` redirection operator:

```cat file1.bin file2.bin file3.bin > combined.bin```

