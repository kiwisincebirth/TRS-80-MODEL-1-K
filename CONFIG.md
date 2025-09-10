# Configuration

## Configuring ROM Paging

The following section applies to Character Font and System ROM's.

The system supports standard (E)EPROM from 128 KBit (16KB) to 512 KBit (64KB)

Depending on the ROM chosen and the use (Char Font/System) multiple pages can be used. 
The following table shows for each combination, the maximum number of pages
that can be programmed and the address bits used for the control of page selection

| Feature                  | Char Font ROM | System ROM |
|--------------------------|---------------|------------|
| Base Image Size          | 4 KB          | 16 KB (*1) |
| Base Address Lines Used  | A0 - A11      | A0 - A13   |
| **Available Pages**      |               |            |
| Max Pages (512 KBit)     | 16            | 4          |
| Max Pages (256 KBit)     | 8             | 2          |
| Max Pages (128 KBit)     | 4             | 1          |
| **Page Addressing**      |               |            |
| Address Lines (512 KBit) | A12 - A15     | A14 - A15  |
| Address Lines (256 KBit) | A12 - A14     | A14        |
| Address Lines (128 KBit) | A12 - A13     | n/a        |

**NOTE 1:** System ROM's require the use of 16 KB, i.e. to be exact power of 2, 
even though typically only the first 12 KB is actually usable by the CPU 

The mapping of the address line(s) is covered below.

### Char Font ROM

Since a character font ROM occupies 4 KB it uses A0-A11 
to address its data, leaving A12-A15 (depending on chip) for page control

**Warning** The silkscreen on the V1 PCB is incorrect. Only use the table below.

| PROM TYPE | SW10 | SW11 | SW12 | SW13  |
|-----------|------|------|------|-------|
| 28256     | ON   | A14  | A13  | A12   |
| 27512     | A14  | A15  | A13  | A12   |
| 27256     | A14  | ON   | A13  | A12   |
| 27128     | ON   | ON   | A13  | A12   |

Notes:
- In V1 of the board DIP Switches were inverted in meaning i.e
  - Switched ON = Logic 0, and switched OFF = Logic 1 
  - This was corrected in V2 and latter revisions, ie. ON=1, OFF=0
- The above table is specifically for V1. For V2 ON should be replaced with OFF

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

When combining ROM images they must be **padded to exactly
16,384 bytes in length**. There are two ways to do this.
* Append a 4 KB file to each ROM image before combining them into final image
* Simply reuse a 4 KB padding file in-between each image in a single copy command.

While not essential I suggest the padding is done with the `FFh` byte.
This leaves the (E)EPROM effectively un-programmed in this area. 
Also (if enabled in future) extending the ROM into the 12KB - 14KB area,
`FFh` gives the maximum backward compatibility, with unoccupied memory.

## Combining ROM Images

The following describes how to combine ROM images at the command line

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

