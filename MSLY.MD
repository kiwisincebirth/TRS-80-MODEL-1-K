
Issues 

External FreHD

When I power off the Model 1K while the FreHD is still on, then when I power on the M1, it has the same screen that it did when I powered it off.
The whole system is locked up, but the screen is intact. The only way I can regain control of it is to power off the M1 and the FreHD and then it returns to normal.  

Diagnosis

When powered off the Model 1K is drawing power from the FreHD.

Powering Off the M1K
- Standalone - Takes voltage to 0v in about 5 seconds.
- FreHD attached and powered - Voltage drops to a minimum of .7v DC in about 15 seconds. It doesn't ever reach 0v.

Apparently the .7v isn't enough to keep anything powered on.

Powering on The M1K
* Before the voltage drops below .85v (about 10 seconds), causes the issue.
* After the voltage drops below .85v, then the system powers on as normal.

If I wait for approximately 15 seconds between power cycles, then it behaves normally.

The original M1 required a 3 second delay before turning it back on.

* Open Collector, doent need a PIC firmware change if use a bodge wire.
* Bleed resistor on main power rail of the computer, AND/OR remove or reduce  the 2200uF on main power rail
Have made change (future) to M1K main power switch (image) so when switched OFF 1-2, 4-5, main 5V rail will be pulled down, rather than left floating. This helps with general orderly shutdown, even without external phantom power

=====

Compatability

====


MIRE with MISE connected 
* boots up.
* Reset button returns to Mem Size instead of a reboot.


With MISE only
* MISE boots up normal.
* Reset button locks system.

Interesting in that the MISE is behaving like the FreHD. Powering off the Rev K and powering it on results in the retained video screen but the computer is locked up.
I can duplicate this over and over with a power cycle until I power off the MISE.

With the MISE and the patched ROM
- no boot at all - just garbage on the screen.
- Even if the MISE is connected to the MIRE nothing boots - 
- When the reset button is pushed, it goes to MEM Size.

Conclusion

I am going to say that the MISE is incompatible with the Rev K.
I am having issues with LDOS not returning from a standard DIR command. 
It doesn't seem to be able to recognize the last drive - just hangs requiring a power cycle on both the MISE and M1K. 
This behavior is not seen on a Rev G.


The MIRE by itself seems to work fine - with the exception of the reset button, which locks up the system.



