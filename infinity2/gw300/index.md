# GW300

![board](board_in_case.jpg)

## Hardware

- Winbond 128MiB SPI NAND 
- LongSung M5710 LTE cat 1 module.
  - CONFIG_USB_NET_RNDIS_HOST
  - CONFIG_USB_SERIAL_OPTION
- ISL1208 RTC
- SIPEX 3232EE RS232 transceiver.
- SP3485 RS485 transceiver.
- p5: seems to be another RS232 serial port
  - 1 ??? 
  - 2 t1out
  - 3 r1in
  - 4 gnd
- dip socket might be for a DTMF generator?

lsusb

```
root@myzr:~# lsusb 
Bus 002 Device 003: ID 2df3:9d03
Bus 001 Device 001: ID 1d6b:0002
Bus 002 Device 001: ID 1d6b:0002
```
