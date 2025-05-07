
# Project Status

## Status

This board has been built, functions, and basic testing has been performed. 
I have tested overnight using the Diagnostic ROM, at both normal and double (3.5Mhz) without any issue
Running Basic ROM, It start's and reports 48KB of ram, I can type and run a basic hello world program. 
Cassette interface is untested at this point. I don't have mass storage at this point so cannot test
any further

There are some small know issue in the board, which have simple corrective items.
This is discussed in the builders guide

## Future

I will likely extend this mainboard some of the items I have in mind are:
* Video snow removal by prioritising Video over CPU access to Video ram
* Onboard Audio amplifier, with speaker output
* Alpha Joystick Port

Lower Priority:
* Inclusion of flexible memory mapping (GAL) to support CP/M...
* Use of paged memory (128KB) using compatible control logic...
* Possible future Model 3 support by remapping (GAL) IO devices...

Before this I want to get mass storage "FreHD" up and running using an internal plug in board.
