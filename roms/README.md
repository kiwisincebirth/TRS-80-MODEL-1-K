# ROM Image Files

## Introduction

The following are some ROM images provided for use in the Model 1k project

Each ROM file is 16Kb in length, and can be appended and written into a paged ROM.

If programming the larger (E)EPROM's you can have 2 or 4 different (paged) ROM images on the same Chip.
When programming each page is 16kB in size, so a 12Kb ROM image needs to padded to 16kB then appended
with the other ROM images you want on the Chip.

For convenience all ROM's included here are 16KB in length

### Level 2 Basic

Two variants are provided
- Level 2 Basic V1.3
- Level 2 Basic V1.3 Patched

The patched version contains the following enhancements
- FreHD Autoboot support.
- Lower Case Mod support. This means that when displaying a character on the screen alphabetic
  character A-Z and a-z are not translated to the 0 - 31 characters. This means that lower case is 
  fully supported and charater roms that have the strange gliphs in the 0 - 31 range are ignored.
- The Reset button (NMI) forces hard reset. This modification removes the normal soft reset 
  (to the READY prompt) on non floppy-disk systems. This is important where an expansion interface 
  is not preset, but a FreHD is connected.

For more information about the patches see [TRS-80 Model 1 ROM Disassembled](https://github.com/kiwisincebirth/TRS-80)

### Diagnostic ROM

The Trs80 Model 1/3 Diagnostic ROM, as featured by Adrian's Digital Basement

See [TRS-80 Diagnostic ROM](https://github.com/misterblack1/trs80-diagnosticrom)

## Combinations

I have included 4 combinations for 32kb and 64 kb ROMS, so including all the files we have the following:

| File             | Bank 1            | Bank 2            | Bank 3            | Bank 4     | Size |
|------------------|-------------------|-------------------|-------------------|------------|------|
| BasicDiag        | Level 2 Basic     | Diagnostic        | -                 | -          | 32k  |
| BasicDiagPatched | Level 2 Basic     | Diagnostic        | Level 2 (Patched) | Diagnostic | 64k  |
| BasicPatched     | Level 2 Basic     | Level 2 (Patched) | -                 | -          | 32k  |
| Level2Basic13    | Level 2 Basic     |                   | -                 | -          | 16k  |
| Level2Patched13  | Level 2 (Patched) |                   | -                 | -          | 16k  |
| PatchedDiag      | Level 2 (Patched) | Diagnostic        | -                 | -          | 32k  |
| trs80m13diag     | Diagnostic        | -                 | -                 | -          | 16k  |


