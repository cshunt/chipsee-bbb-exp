chipsee-bbb-exp
===============

I try to develop some Device Tree Overlays for the Chipsee Expansion Board with the 7" LCD, Touchscreen, Accelerometer, CAN and RS232 for the BeagleBone black.

Devices on the cape
===================

- [x] User LED's (see https://github.com/dl7tny/chipsee-bbb-exp#chipsee-leddts)
- [ ] User Beeper
- [ ] User Buttons
- [ ] Accelerometer (ADXL345)
- [ ] LC Display (DS90C385)
- [ ] Capacitive Touchscreen (FT5306DE4)
- [ ] Audio In and Out (TLV320AIC3106)
- [ ] RS232
- [ ] RS485
- [ ] CAN Bus


Compiling
=========
To compile the dts files to the dtbo files, you need the device tree compiler, with patches for the BBB. Information about compiling and getting the compiler can be found at http://learn.adafruit.com/introduction-to-the-beaglebone-black-device-tree/compiling-an-overlay


CHIPSEE-LED.dts
===============

The board has two front panel LED labeled D1 (blue) and D2 (green). After compiling and importing the device tree overlay, they can be accessed like the four led on the BeagleBone black via the folders 

 * /sys/class/leds/chipsee:led:d1
 * /sys/class/leds/chipsee:led:d2

You can even set the triggers for these LED like you would do for the normal BeagleBone LED by inserting the trigger into the file trigger. For example to have the heartbeat at your green LED type:

```
echo heartbeat > /sys/class/leds/chipsee\:led\:d2
```