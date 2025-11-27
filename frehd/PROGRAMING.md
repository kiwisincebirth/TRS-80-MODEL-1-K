
# Programming PIC

## Download the FreHD firmware

Downloading
* https://github.com/ontheslab/FreHDv1CPM
* Click "Tags" and the latest (e.g. 2.17) firmware
* download and uncompress the ZIP file 
* The fie you need has a HEX extension

## PicKit 3

I ordered a PicKit 3.5 from China which came with a small PCB containing a 40 pin ZIP socket
to which the PIC chip can be inserted.

Programming is done Either
* connect pickit directly to programming header on the FreHD board
* connect pickit to the supplied 40 pin ZIF socket (provided) board placing the PIC chip in the socket

I would recommend the first option since you don't have to remove this chip from the FreHD board

Software Download
* As of writing 6.25 (and newer) is not compatible with pickit 3
* download and Install Mp LAB X version 6.20
* https://www.microchip.com/en-us/tools-resources/archives/mplab-ecosystem

Software Installation
* You only need to install the 
* IPE (programming environment)
* 8 bit CPU support

The IDE is not needed since FreHD was written on a much earlier software dev platform
the compiler that it installs is incompatible, think.

## Run MPLab IPE

To give the full advanced UI, choose Menu "Settings / Advanced Mode",
then enter the default password and tick box about not logging out

POWER OPTIONS
* Select - Power target from PIC - means power is provided by the programmer

OPERATE 
* answer some basic questions 
 
| Attribute | Value               |
|-----------|---------------------|
| Family    | Advanced 8bit CPU's |
| Device    | PIC18F4620          |
| Tool      | PICKit3             |

Then 
* Press Connect this should download configure the programmer itself, this may take a while
* Use the Browse select the HEX file you downloaded earlier
* Program
* Verify


