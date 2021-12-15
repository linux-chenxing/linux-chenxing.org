# DongShanPi One

![board](board.jpg)

## Specs

- SSD202D
- 0.9/1.0V core voltage control
- USB-C host port (usb1)
- CP2104 usb->serial (usb2)
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
## Working USB devices

- WAVLINK WL-NWU327GC - USB-C gigabit ethernet 
  - [amazon.jp](https://www.amazon.co.jp/WAVLINK-%E6%9C%89%E7%B7%9ALAN%E3%82%A2%E3%83%80%E3%83%97%E3%82%BF%E3%83%BC-%E3%82%AE%E3%82%AC%E3%83%93%E3%83%83%E3%83%88%E3%82%A4%E3%83%BC%E3%82%B5%E3%83%8D%E3%83%83%E3%83%88%E5%A4%89%E6%8F%9B%E3%82%A2%E3%83%80%E3%83%97%E3%82%BF%E3%83%BC-1000Mbps-11-X%E3%80%81Linux%E3%80%81Chrome/dp/B09FFK844R)
  - [banggood](https://usa.banggood.com/WAVLINK-USB-3_1-Type-C-or-USB3_0-to-Gigabit-Ethernet-Adapter-USB3_0-to-LAN-RJ45-Port-Converter-5Gbps-Network-Connector-p-1910699.html?cur_warehouse=CN&ID=529723)

