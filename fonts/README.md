# Font Files

## Introduction

The following are some character generator fonts for use

Each font file is 4Kb (4,096 bytes) in length, and should be appended if burning  

### Character Set 06, 08, 14, 15

These are traditional font sets and are documented here: 

[Character Generator Roms](https://github.com/RetroStack/Character_Generator_ROMs/tree/main/TRS-80%20Model%201/Individual)

Each font has 2 versions
* Original - Is the original font converted to the correct 4KB format, but otherwise unmodified.
* Final - Is a modified font as per below.

The modified Final fonts have the following changes:
* The punctuation characters  , : ;  moved vertically down for correct alignment.
* The lower case characters  g j p q y ) are stretched to have 2 line decenders

In summary each character has 
* 1 leading blank line
* 7 Lines for body of the character
* 2 line for decenders
* 2 trailing blank lines

ORIGINAL (example)

(FONT-Orig.jpg)

FINAL (example)

(FONT-NEW.jpg)

### Glens Character Rom

This is an unmodified copy 9which is compatable) of the font file used in the following project

[Glens Stuff TRS-80 Clone](https://www.glensstuff.com/trs80/trs80.htm)

### Graphics 8 bit Font

In a regular TRS-80 64 characters of the regualr font are assigned to represent graphic pixels in a 2 x 3 matrix.
This gives a total of 6 pixels per character, each pixel utilises 3 hozizontal and 4 vertical raster sub-pixels
The total screen resolution is 128 x 48

In this font, we assign all 256 characters to be graphics characters to render gaphics in a 2 x 4 matrix 
This means each graphic pixel would be 3x3 actual raster pixels on the screen, with a total resolution of
128 x 64 pixels, a 33% improvement, 

This is an experimental font, not much use at present.
Just needs a software controllable Bit for regular or enhanced graphics

One advantage would be existing software could easily make use of it, just need to redefine which character to write to the screen,
and when to switch into and out of this new font, nothing much else changes.
The downsides is that you cant show any text characters on the screen at the same time.


