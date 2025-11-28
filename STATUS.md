
# Project Status

## 28 Nov 2025

Added Floppy 80 board

## 4 Nov 2025

MSly has reported a issue with CPU speed selection causing hanging. See [Known Issues](./KNOWN_ISSUES.md)

## 25 Oct 2025

After almost 6 months V2 of the Model 1k is out. It provides significant
improvements in video, not only does it use dual port RAM for snow free video, 
but it changes the video sync generation circuit bringing back the picture 
adjustment controls not present in V1. Also supported is software switchable 
fonts, for alternate languages or other graphics. Other major features added to the board 
include an audio amplifier for a small speaker (which can be mounted on the board), 
Alpha Joystick port compatible with most software, and ability to mount a modern clock oscillator.
Have added about 10 new config jumpers/settings in support of new features.
V1 is still fully supported including a separate build guide.
Not forgetting Supermem bank RAM and internal FreHD

## 23 Oct 2025

Completed Final assembly and testing of V2 board. Published to GITHUB

## 18 Oct 2025

Major milestones today 
* completed work on the Supermem board, which is now fully documented.
* Got the V2 prototype up and running. 

## 29 Sept 2025

I have now published a V1c of the board that fixes some minor issues.
* The issue in the silkscreen for Character Generator Dip Switches
* Added a mounting hole to allow [FreHD](./frehd/README.md) board to better held in place 

## 24 Sept 2025

Ordered the V2 boards

## Update 10 Sept 2025

A couple of items to report
* Just had a report of a an independent build of the board by "MSly" - reported on Tandy Discord
* I have added a couple of new documents to the project 
  * [Troubleshooting](./TROUBLESHOOT.md), which aims to give some guidance of things to check if not working
  * [Config](./CONFIG.md), showing a bit about how to program ROMS
  * [Compatability](./COMPATABILITY.md), showing things that have been tested and know to work (or not)

## Update 3 Sept 2025

An individual PCB can now be ordered from [Tuc's Workbench](https://shop.tucs-workbench.com/products/trs-80-model-i-revision-k)

## Update 1 Sept 2025

Added a new Folder "Roms" to the project.

## Update 28th August 2025

I have now published a V1b of the board that fixes some additional minor issues in V1.
This also improves the BOM to include full component identifiers suitable for ordering.
There is also some improvements backported from V2 - Please see the [Changelog](CHANGELOG.md)
This release also includes the Kicad files, since this is the last V1 release I intend to make.

Noting I think there is an issue in the silkscreen for Character Generator Dip Switches
the silkscreen should read.

```
PROM TYPE  SW10  SW11  SW12  SW13
28256      OFF   A14   A13   A12
27512      A14   A15   A13   A12
27256      A14   OFF   A13   A12
27128      OFF   OFF   A13   A12
```

## Update 9th August 2025

I have now published a V1a of the board that fixes the minor issues found in V1 of the board

## Status July 2025

Working on V2 of the board, this is an ongoing process. See the changelog for an updated 
list of changes in V2

## Status June 2025

"FreHD" is up and running using an internal plug in board, and is document on this Repository.
I am likely to spend some time relearning some of the aspects of DOS on trs-80

I have started on V2 the feature list is documented in the (Changelog)[./CHANGELOG.md], 
and includes most of the high priority items below.

One item I am still considering is the inclusion of simpler Sync generation with
adjustable Positional controls.

## Status May 2025

This board has been built, functions, and basic testing has been performed. 
I have tested overnight using the Diagnostic ROM, at both normal and double (3.5Mhz) without any issue
Running Basic ROM, It start's and reports 48KB of ram, I can type and run a basic hello world program. 
Cassette interface is untested at this point. I don't have mass storage at this point so cannot test
any further

There are some small know issue in the board, which have simple corrective items.
This is discussed in the builders guide

### Future

I will likely extend this mainboard some of the items I have in mind are:
* Video snow removal by prioritising Video over CPU access to Video ram
* Onboard Audio amplifier, with speaker output
* Alpha Joystick Port

Before this I want to get mass storage "FreHD" up and running using an internal plug in board.

### Lower Priority:
* Inclusion of flexible memory mapping (GAL) to support CP/M...
* Use of paged memory (128KB) using compatible control logic...
* Possible future Model 3 support by remapping (GAL) IO devices...

