# DongShanPi One

![board](board.jpg)

## Specs

- SSD202D
- 0.9/1.0V core voltage control
- CP2104 usb->serial
- USB-C port (host)
- XCSP1AAWH-NT 128MB SPI NAND flash
- 1 x GPIO button
- 2 x GPIO controlled LEDs (third LED is power)
- RGB LCD connector

## Flashing

With an i2c dongle and the mstar enabled SNANDer fork:

```
sudo ./SNANDer -p mstarddc -c /dev/i2c-4:49 -e
sudo ./SNANDer -p mstarddc -c /dev/i2c-4:49 -w GCIS.bin
sudo ./SNANDer -p mstarddc -c /dev/i2c-4:49 -a 0x140000 -l 0x54C0 -w IPL.bin
sudo ./SNANDer -p mstarddc -c /dev/i2c-4:49 -a 0x200000 -l 0xBF58 -w ~/idosom2d01-ipl
```
