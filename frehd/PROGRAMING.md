
# Programming PIC

## Download the FreHD firmware

Downloading
* https://github.com/ontheslab/FreHDv1CPM
* Click "Tags" and the latest (e.g. 2.17) firmware
* download and uncompress the ZIP file 
* The fie you need has a HEX extension

## PicKit 3

I ordered a PicKit 3.5 from China
* It came with a small PCB containing a 40 pin ZIP socket
* set jumpers for 40 pin operation J1:A J2:2-3 J3:2-3
* connect pickit to small PCB - MCLR on board is Pin 1 (triangle on Pickit)

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


