chipsee-bbb-exp
===============

I try to develop some Device Tree Overlays for the Chipsee Expansion Board with the 7" LCD, Touchscreen, Accelerometer, CAN and RS232 for the BeagleBone black.


CHIPSEE-LED.dts
===============
Supports the two front panel LED. After compiling and importing the overlay, the LED can be accessed via the folders /sys/class/leds/chipsee:led:d1 and /sys/class/leds/chipsee:led:d2.