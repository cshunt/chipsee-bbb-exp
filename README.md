chipsee-bbb-exp
===============

Working with CaptainStouf's github files I am expanding on a device tree for the beaglebone black to operate the 7in lcd,  The Device Tree Overlays is for the Chipsee Expansion Board with the 7" LCD, Touchscreen, Accelerometer, CAN and RS232 for the BeagleBone black. 1024x600 lcd, model EXP7H.

Devices on the cape
===================

- [x] User LED's 
- [ ] User Buzzer 
- [x] User Buttons
- [ ] Accelerometer (ADXL345)
- [x] LC Display (DS90C385)
- [x] Capacitive Touchscreen (FT5306DE4)
- [ ] Audio In and Out (TLV320AIC3106)
- [ ] RS232
- [ ] RS485
- [ ] CAN Bus


Compiling
=========

https://github.com/beagleboard/bb.org-overlays
Copy to directory, dts source file should be located in /src/arm/
while in main directory run "make", this will generate dtbo file, copy this file to /lib/firmware/ directory
update /boot/uEnv.txt to include the new dtbo file, device tree overlay.
there should be a line such as "uboot_overlay_addr0=/lib/firmware/CHIPSEE-TOUCH_C.dtbo"

Previous reference - may be dated
//To compile the dts files to the dtbo files, you need the device tree compiler, with patches for the BBB. Information about //compiling and getting the compiler can be found at http://learn.adafruit.com/introduction-to-the-beaglebone-black-device-//tree/compiling-an-overlay




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

CHIPSEE-TOUCH_C.dts
==================

This device tree is based off the BB-BONE-4D7C-01-00A1.dts with changes from the older chipsee dtb file floating around that doesn't seem to compile. LCD is functioning, Touchscreen for capacitance touch is working x, y, were swapped and inverted, to get a good touch screen response, the size y is beyond the 600 pixel screen size.
