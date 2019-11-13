# HX711-Device-Tree-Overlay

This device tree overlay allows you to connect an [HX711 load sensing amplifier](https://www.sparkfun.com/products/13879) to GPIO23 and GPIO24 pins on an Raspberry Pi A+.

SCK -> GPIO23

DOUT -> GPIO24

The hx711 is a combined A2D converter and amplifier commonly connected to load sensors.

This was an especially difficult task because the hx711 is a bit banging device. It is not hooked into the i2c or SPI systems as usual, instead it is hooked into the Raspberry Pi's pinctrl subsystem.

There are several steps in this process including:

1) Use menuconfig to activate the driver and rebuild the kernel

2) Build the dtbo file like so:
```
dtc -@ -I dts -O dtb -o hx711.dtbo hx711.dts
```
3) Add the line ```dtoverlay=hx711``` to your config.txt file

Then you should be able to communicate with the HX711 through sysfs.
