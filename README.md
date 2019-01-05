chipsee-bbb-exp
===============

I try to develop some Device Tree Overlays for the Chipsee Expansion Board with the 7" LCD, Touchscreen, Accelerometer, CAN and RS232 for the BeagleBone black.

Devices on the cape
===================

- [ ] User LED's (see https://github.com/dl7tny/chipsee-bbb-exp#chipsee-leddts)
- [ ] User Buzzer (see https://github.com/dl7tny/chipsee-bbb-exp#chipsee-buzzerdts)
- [ ] User Buttons
- [ ] Accelerometer (ADXL345)
- [x] LC Display (DS90C385)
- [x] Capacitive Touchscreen (FT5306DE4)
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
echo heartbeat > /sys/class/leds/chipsee\:led\:d2/trigger
```

CHIPSEE-BUZZER.dts
==================

The buzzer on the chipsee expansion is connected to Pin 8 of Header P8 and is working as a simple gpio pin. To configure the pin, compile and load the device tree overlay and then run the following commands:


```
echo 67 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio67/direction
```

You can use the buzzer with the following commands
```
enable: echo 1 > /sys/class/gpio/gpio67/value
disable: echo 0 > /sys/class/gpio/gpio67/value 
```

P.S. If you do not hear anything, then first remove the 'REMOVE AFTER WASHING' label and then push the buzzer soft against the board. The buzzer on my board was not soldered to the board correctly.
