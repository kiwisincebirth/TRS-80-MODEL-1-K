# Font Files

## Introduction

The following are some character generator fonts for use

Each font file is 4Kb (4,096 bytes) in length, and should be appended if burning  

### General Character Sets

These four traditional font sets (and 2 new derivitives) and are documented here: 

[Character Generator Roms](https://github.com/RetroStack/Character_Generator_ROMs/tree/main/TRS-80%20Model%201/Individual)

In Summary:
* 06 - no duplicates, [ \ ] ^ ` ~
* 08 - no duplicates, ↑ ↓ ← → £/¥
* 14 - duplicates AZ, [ \ ] ^ ` ~
* 15 - duplicates AZ, ↑ ↓ ← → £/¥
* 17 - no duplicates, ↑ ↓ ← → ` ~ (derivative)
* 18 - duplicates AZ, ↑ ↓ ← → ` ~ (derivative)

Each font has 2 versions
* Original - Is the original font converted to the correct 4KB format, but otherwise unmodified.
* Final - Is a modified font as per below.

The modified Final fonts have the following changes:
* The punctuation characters  . , : ;  moved vertically down for correct alignment.
* The lower case characters  g j p q y  are stretched to have 2 line decenders
* All characters are moved down by 1 pixel, leaving a blank first raster line
* The last character (hex 7F) expands to fill the entire 6 by 12 matrix

The following shows how these changes apply differences

![Font Changes](Font-Changes.png)

In summary each character has 
* 1 leading blank line
* 7 Lines for body of the character
* 2 line for descenders
* 2 trailing blank lines

ORIGINAL (example)

![Original Font](Font-Original.jpg)

FINAL (example)

![Final Font](Font-New.jpg)

### GenDon3

This is an unmodified copy of "two" of the fonts provided by the GenDon3 hardware modification

* GenDon3-61 - I would suggest going with Dash 61 with the real underscore, for better ASCII compatibility.
* GenDon3-6A (not provided) - has differences in the characters ' , ; V j m. The three punctuation marks are too far to the right, and the semicolon appears to be missing a pixel
* GenDon3-9E - The only difference between 9E and Dash 61 is that Dash 61 has a real underscore at the ASCII underscore code (95), where 9E has a four-line-high lump. They both have the lump at code 31

See The following discussion:

[GENDON3 improved character generator for the Model I](https://forum.vcfed.org/index.php?threads/gendon3-improved-character-generator-for-the-model-i-discussion.59498)

### Glens Character Rom

This is an unmodified copy 9which is compatible) of the font file used in the following project

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


